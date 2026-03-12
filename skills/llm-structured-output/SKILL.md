---
name: llm-structured-output
description: >
  Get reliable JSON, enums, and typed objects from LLMs using response_format, tool_use, and schema-constrained decoding across OpenAI, Anthropic, and Google APIs.
risk: safe
source: community
date_added: "2026-03-12"
---

# LLM Structured Output

## What This Skill Does

Extract typed, validated data from LLM API responses instead of parsing free-text. This skill covers the three main approaches: OpenAI's `response_format` with JSON Schema, Anthropic's `tool_use` block for structured extraction, and Google's `responseSchema` in Gemini. You will learn when each approach works, when it breaks, and how to build retry logic around schema validation failures that every production system encounters.

## When to Use This Skill

- The user needs to extract structured data (JSON objects, arrays, enums) from an LLM response
- The user is building a pipeline where LLM output feeds directly into code (database writes, API calls, UI rendering)
- The user asks about `response_format`, `json_mode`, `json_object`, or `json_schema` in OpenAI
- The user asks about using Anthropic's `tool_use` or `tool_result` blocks for data extraction (not for actual tool execution)
- The user asks about Zod schemas with `zodResponseFormat()` from the `openai` npm package
- The user needs to parse LLM output into Pydantic models using `instructor`, `marvin`, or manual validation
- The user is getting malformed JSON, missing fields, or wrong types from LLM responses and needs a fix
- The user asks about `controlled generation`, `constrained decoding`, or `grammar-based sampling` in local models

Do NOT use this skill when:
- The user wants free-form text generation (summaries, essays, chat)
- The user is asking about Zod for form validation or API input validation (use `zod-validation-expert` instead)
- The user needs prompt engineering for better text quality (not structure)
- The user wants to call real external tools/APIs (this skill covers using tool_use as a structured output hack, not actual tool orchestration)

## Core Workflow

1. Identify the target schema. Ask the user what fields they need extracted. Define every field with its type, whether it's required or optional, and valid enum values if applicable. Do not proceed without a concrete schema.

2. Choose the provider-appropriate method:
   - **OpenAI (gpt-4o, gpt-4o-mini):** Use `response_format: { type: "json_schema", json_schema: { ... } }`. This enables Structured Outputs with guaranteed schema conformance via constrained decoding.
   - **Anthropic (Claude):** Define a single tool with the target schema as `input_schema` and set `tool_choice: { type: "tool", name: "extract_data" }`. Claude returns the structured data in the `tool_use` content block.
   - **Google (Gemini):** Use `generationConfig.responseSchema` with a JSON Schema object and set `responseMimeType: "application/json"`.
   - **Local models (llama.cpp, vLLM):** Use GBNF grammars or `--json-schema` flag for constrained decoding at the token level.

3. Write the schema definition in the user's language. For Python, define a Pydantic `BaseModel`. For TypeScript, define a Zod schema and convert it with `zodResponseFormat()`. For raw API calls, write JSON Schema directly.

4. Include field-level descriptions in the schema. Every field should have a `description` string that tells the model what to put there. Models use these descriptions as implicit prompt instructions — a field described as `"The user's sentiment as positive, negative, or neutral"` produces better results than a bare `sentiment: str` with no context.

5. Set the system prompt to reinforce structure. Tell the model its job is data extraction, not conversation. Example: `"You are a data extraction system. Analyze the input and return the requested fields. Do not include explanations outside the JSON structure."`

6. If using OpenAI's `json_schema` mode, set `"strict": true` in the schema definition. This activates constrained decoding where the model can only output tokens that conform to the schema. Without `strict: true`, the model may still produce invalid JSON.

7. If using Anthropic's tool_use approach, extract the structured data from `response.content` by finding the block where `type == "tool_use"` and reading its `input` field. Do not parse the text blocks — the structured data lives exclusively in the tool_use block.

8. Validate the response against the schema in your application code. Even with constrained decoding, validate with Pydantic's `model_validate()` or Zod's `.parse()` before passing data downstream. This catches semantic issues (empty strings, out-of-range numbers) that schema conformance alone cannot prevent.

9. Build a retry loop for validation failures. When validation fails, send the original input plus the failed output and the validation error back to the model with an instruction like `"Your previous output failed validation: {error}. Fix the output."` Cap retries at 3 attempts.

10. Log every structured output call with: the input, the raw response, the parsed result, and any validation errors. When structured output breaks in production, you need these logs to determine whether the failure was a schema design issue, a prompt issue, or a model regression.

## Examples

### Example 1: OpenAI Structured Outputs with Pydantic (Python)

```python
from pydantic import BaseModel, Field
from openai import OpenAI
from enum import Enum

class Sentiment(str, Enum):
    positive = "positive"
    negative = "negative"
    neutral = "neutral"

class ReviewAnalysis(BaseModel):
    sentiment: Sentiment = Field(description="Overall sentiment of the review")
    key_topics: list[str] = Field(description="Main topics mentioned, max 5")
    purchase_intent: bool = Field(description="Whether the reviewer would buy again")
    confidence_score: float = Field(ge=0.0, le=1.0, description="Model confidence 0-1")

client = OpenAI()
response = client.beta.chat.completions.parse(
    model="gpt-4o-2024-08-06",
    messages=[
        {"role": "system", "content": "Extract structured review analysis."},
        {"role": "user", "content": "This laptop is amazing. The battery lasts forever and the keyboard feels great. Definitely buying the next version."}
    ],
    response_format=ReviewAnalysis,
)
result = response.choices[0].message.parsed
# result.sentiment == Sentiment.positive
# result.key_topics == ["battery life", "keyboard"]
# result.purchase_intent == True
```

### Example 2: Anthropic tool_use for Structured Extraction (Python)

```python
import anthropic

client = anthropic.Anthropic()
response = client.messages.create(
    model="claude-sonnet-4-20250514",
    max_tokens=1024,
    system="You are a data extraction system. Use the provided tool to return structured data.",
    tools=[{
        "name": "extract_invoice",
        "description": "Extract invoice fields from text",
        "input_schema": {
            "type": "object",
            "properties": {
                "vendor_name": {"type": "string", "description": "Company that issued the invoice"},
                "total_amount": {"type": "number", "description": "Total amount in USD"},
                "line_items": {
                    "type": "array",
                    "items": {
                        "type": "object",
                        "properties": {
                            "description": {"type": "string"},
                            "quantity": {"type": "integer"},
                            "unit_price": {"type": "number"}
                        },
                        "required": ["description", "quantity", "unit_price"]
                    }
                }
            },
            "required": ["vendor_name", "total_amount", "line_items"]
        }
    }],
    tool_choice={"type": "tool", "name": "extract_invoice"},
    messages=[{"role": "user", "content": "Invoice from Acme Corp: 3x Widget A at $10 each, 1x Widget B at $25. Total: $55."}]
)
# Find the tool_use block — do NOT parse text blocks
tool_block = next(b for b in response.content if b.type == "tool_use")
invoice = tool_block.input
# invoice["vendor_name"] == "Acme Corp"
# invoice["total_amount"] == 55.0
```

### Example 3: TypeScript with Zod + zodResponseFormat

```typescript
import OpenAI from "openai";
import { z } from "zod";
import { zodResponseFormat } from "openai/helpers/zod";

const EventSchema = z.object({
  event_name: z.string().describe("Name of the event"),
  date: z.string().describe("ISO 8601 date string"),
  location: z.string().describe("City and venue"),
  attendee_count: z.number().int().describe("Expected number of attendees"),
  is_virtual: z.boolean().describe("Whether the event is online-only"),
});

const client = new OpenAI();
const completion = await client.beta.chat.completions.parse({
  model: "gpt-4o-2024-08-06",
  messages: [
    { role: "system", content: "Extract event details from the text." },
    { role: "user", content: "Tech Summit 2025 in Austin at the Convention Center on March 15th. Expecting 2000 attendees, in-person only." },
  ],
  response_format: zodResponseFormat(EventSchema, "event_extraction"),
});
const event = completion.choices[0].message.parsed;
// event.event_name === "Tech Summit 2025"
// event.is_virtual === false
```

## Never Do This

## Edge Cases

## Best Practices
