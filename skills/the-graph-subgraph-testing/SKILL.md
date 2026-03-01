---
name: the-graph-subgraph-testing
description: "Use when testing a subgraph on The Graph with Matchstick unit tests, Subgraph Linter static analysis, or CI/CD pipelines. Covers mock events, entity assertions, and contract mocks."
risk: low
source: "PaulieB14/subgraphs-skills (MIT)"
date_added: "2026-03-01"
---

# The Graph — Subgraph Testing

You're an expert in subgraph quality assurance. You've caught division-by-zero bugs with the linter before they crashed production. You've written Matchstick tests that found entity overwrite bugs that would have corrupted data silently for months.

Your hard-won lessons: The team that skipped linting had a subgraph crash on mainnet from a force-unwrapped null. The team that didn't test their handlers shipped broken P&L calculations for weeks. Static analysis + unit tests catch 90% of issues before deployment.

## When to Use

Use when the user asks to:
- Write unit tests for subgraph mapping handlers
- Use Matchstick testing framework
- Run Subgraph Linter static analysis
- Mock blockchain events or contract calls
- Assert entity field values in tests
- Set up CI/CD for a subgraph project
- Catch null pointer, division-by-zero, or entity overwrite bugs

## Quick Start

```bash
npm install --save-dev matchstick-as
graph test                    # Run all tests
graph test mapping            # Run specific test file
graph test -c                 # With coverage
```

## Subgraph Linter (run this first)

Catches runtime bugs at compile time — run before every commit.

```bash
git clone https://github.com/graphprotocol/subgraph-linter.git
cd subgraph-linter && npm install && npm run build
npm run check -- --manifest ../your-subgraph/subgraph.yaml
```

Key checks it catches:

| Bug | Pattern |
|-----|---------|
| Null crash | `Entity.load(id)!` without null check |
| Entity overwrite | Helper saves entity, then caller saves stale copy |
| Division by zero | `a.div(b)` where b could be zero |
| Undeclared eth_call | Contract call not in manifest `calls:` block |

```typescript
// BAD — crashes if entity doesn't exist
let token = Token.load(address)!

// GOOD — explicit null check
let token = Token.load(address)
if (token == null) {
  token = new Token(address)
  token.totalSupply = BigInt.zero()
}
```

## Matchstick Unit Tests

### Basic test structure

```typescript
import { describe, test, afterEach, clearStore, assert } from "matchstick-as"
import { handleTransfer } from "../src/mapping"

describe("Transfer Handler", () => {
  afterEach(() => { clearStore() })  // Always clear between tests

  test("creates Transfer entity", () => {
    let event = createTransferEvent(from, to, BigInt.fromI32(1000))
    handleTransfer(event)
    assert.entityCount("TransferEvent", 1)
    assert.fieldEquals("TransferEvent", id, "value", "1000")
  })
})
```

### Creating mock events

```typescript
import { newMockEvent } from "matchstick-as"
import { ethereum, Address, BigInt } from "@graphprotocol/graph-ts"
import { Transfer } from "../generated/ERC20/ERC20"

export function createTransferEvent(from: Address, to: Address, value: BigInt): Transfer {
  let event = changetype<Transfer>(newMockEvent())
  event.parameters = [
    new ethereum.EventParam("from", ethereum.Value.fromAddress(from)),
    new ethereum.EventParam("to", ethereum.Value.fromAddress(to)),
    new ethereum.EventParam("value", ethereum.Value.fromUnsignedBigInt(value))
  ]
  event.block.timestamp = BigInt.fromI32(1640000000)
  event.transaction.hash = Bytes.fromHexString("0xabc123...")
  return event
}
```

### Mocking contract calls

```typescript
import { createMockedFunction } from "matchstick-as"

createMockedFunction(contractAddress, "name", "name():(string)")
  .returns([ethereum.Value.fromString("My Token")])

createMockedFunction(contractAddress, "decimals", "decimals():(uint8)")
  .returns([ethereum.Value.fromI32(18)])

// Mock a revert
createMockedFunction(contractAddress, "name", "name():(string)").reverts()
```

### Assertions

```typescript
assert.entityCount("Token", 1)
assert.fieldEquals("Token", tokenId, "name", "My Token")
assert.fieldEquals("Token", tokenId, "decimals", "18")
assert.fieldEquals("Transfer", id, "value", "1000000000000000000")
assert.notInStore("Token", "nonexistent-id")
```

## CI/CD Pipeline

```yaml
# .github/workflows/test.yml
name: Test Subgraph
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with: { node-version: '18' }
      - run: npm ci
      - run: npm run codegen
      - run: npm run check -- --manifest subgraph.yaml  # Linter
      - run: npm test                                    # Matchstick
      - run: npm run build
```

## Usage Examples

```
"Write Matchstick tests for my Transfer event handler"
"Run the Subgraph Linter on my project"
"How do I mock a contract call in my tests?"
"Set up CI/CD for my subgraph with GitHub Actions"
"My subgraph crashes with a null error, how do I find it?"
```

## References

- [Matchstick Docs](https://thegraph.com/docs/en/subgraphs/developing/creating/unit-testing-framework/)
- [Subgraph Linter](https://thegraph.com/docs/en/subgraphs/developing/subgraph-linter/)
- [Subgraph Uncrashable](https://thegraph.com/docs/en/subgraphs/developing/subgraph-uncrashable/)
