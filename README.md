<!-- registry-sync: version=7.0.1; skills=1206; stars=21178; updated_at=2026-03-07T08:34:18+00:00 -->
# 🌌 Antigravity Awesome Skills: 1,206+ Agentic Skills for Claude Code, Gemini CLI, Cursor, Copilot & More

> **The Ultimate Collection of 1,206+ Universal Agentic Skills for AI Coding Assistants — Claude Code, Gemini CLI, Codex CLI, Antigravity IDE, GitHub Copilot, Cursor, OpenCode, AdaL**

[![GitHub stars](https://img.shields.io/badge/⭐%2021%2C000%2B%20Stars-gold?style=for-the-badge)](https://github.com/sickn33/antigravity-awesome-skills/stargazers)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Anthropic-purple)](https://claude.ai)
[![Gemini CLI](https://img.shields.io/badge/Gemini%20CLI-Google-blue)](https://github.com/google-gemini/gemini-cli)
[![Codex CLI](https://img.shields.io/badge/Codex%20CLI-OpenAI-green)](https://github.com/openai/codex)
[![Kiro](https://img.shields.io/badge/Kiro-AWS-orange)](https://kiro.dev)
[![Cursor](https://img.shields.io/badge/Cursor-AI%20IDE-orange)](https://cursor.sh)
[![Copilot](https://img.shields.io/badge/GitHub%20Copilot-VSCode-lightblue)](https://github.com/features/copilot)
[![OpenCode](https://img.shields.io/badge/OpenCode-CLI-gray)](https://github.com/opencode-ai/opencode)
[![Antigravity](https://img.shields.io/badge/Antigravity-DeepMind-red)](https://github.com/sickn33/antigravity-awesome-skills)
[![AdaL CLI](https://img.shields.io/badge/AdaL%20CLI-SylphAI-pink)](https://sylph.ai/)
[![ASK Supported](https://img.shields.io/badge/ASK-Supported-blue)](https://github.com/yeasy/ask)
[![Web App](https://img.shields.io/badge/Web%20App-Browse%20Skills-blue)](apps/web-app)
[![Buy Me a Book](https://img.shields.io/badge/Buy%20me%20a-book-d13610?logo=buymeacoffee&logoColor=white)](https://buymeacoffee.com/sickn33)

**Antigravity Awesome Skills** is a curated, battle-tested library of **1,206+ high-performance agentic skills** designed to work seamlessly across the major AI coding assistants.

**Welcome to the V7.0.1 21k Stars Patch Release!** This repository gives your agent reusable playbooks for planning, coding, debugging, testing, security review, infrastructure work, product thinking, and much more.

> **🌟 21,000+ GitHub Stars Milestone!** Thank you to the community for turning this into one of the largest skill libraries in this category.

## Table of Contents

- [Quick Start](#quick-start)
- [Choose Your Tool](#choose-your-tool)
- [What This Repo Includes](#what-this-repo-includes)
- [Project Structure](#project-structure)
- [Top Starter Skills](#top-starter-skills)
- [Three Real Examples](#three-real-examples)
- [Browse 1,204+ Skills](#browse-1204-skills)
- [Documentation](#documentation)
- [Web App](#web-app)
- [Contributing](#contributing)
- [Community](#community)
- [Support the Project](#support-the-project)
- [Credits & Sources](#credits--sources)
- [Repo Contributors](#repo-contributors)
- [License](#license)
- [Star History](#star-history)

## Quick Start

1. Install once:

```bash
npx antigravity-awesome-skills
```

2. Verify the default install:

```bash
test -d ~/.gemini/antigravity/skills && echo "Skills installed"
```

3. Use your first skill:

```text
Use @brainstorming to plan a SaaS MVP.
```

4. Browse starter collections in [`docs/users/bundles.md`](docs/users/bundles.md) and execution playbooks in [`docs/users/workflows.md`](docs/users/workflows.md).

## Choose Your Tool

| Tool | Install | First Use |
| --- | --- | --- |
| Claude Code | `npx antigravity-awesome-skills --claude` | `>> /brainstorming help me plan a feature` |
| Cursor | `npx antigravity-awesome-skills --cursor` | `@brainstorming help me plan a feature` |
| Gemini CLI | `npx antigravity-awesome-skills --gemini` | `Use brainstorming to plan a feature` |
| Codex CLI | `npx antigravity-awesome-skills --codex` | `Use brainstorming to plan a feature` |
| Antigravity | `npx antigravity-awesome-skills --antigravity` | `Use @brainstorming to plan a feature` |
| Kiro CLI | `npx antigravity-awesome-skills --kiro` | `Use brainstorming to plan a feature` |
| Kiro IDE | `npx antigravity-awesome-skills --path ~/.kiro/skills` | `Use @brainstorming to plan a feature` |
| GitHub Copilot | _No installer — paste skills or rules manually_ | `Ask Copilot to use brainstorming to plan a feature` |
| OpenCode | `npx antigravity-awesome-skills --path .agents/skills` | `opencode run @brainstorming help me plan a feature` |
| AdaL CLI | `npx antigravity-awesome-skills --path .adal/skills` | `Use brainstorming to plan a feature` |
| Custom path | `npx antigravity-awesome-skills --path ./my-skills` | Depends on your tool |

## What This Repo Includes

- **Skills library**: `skills/` contains the reusable `SKILL.md` collection.
- **Installer**: the npm CLI installs skills into the right directory for each tool.
- **Catalog**: [`CATALOG.md`](CATALOG.md), `skills_index.json`, and `data/` provide generated indexes.
- **Web app**: [`apps/web-app`](apps/web-app) gives you search, filters, rendering, and copy helpers.
- **Bundles**: [`docs/users/bundles.md`](docs/users/bundles.md) groups starter skills by role.
- **Workflows**: [`docs/users/workflows.md`](docs/users/workflows.md) gives step-by-step execution playbooks.

## Project Structure

| Path | Purpose |
| --- | --- |
| `skills/` | The canonical skill library |
| `docs/users/` | Getting started, usage, bundles, workflows, visual guides |
| `docs/contributors/` | Templates, anatomy, examples, quality bar, community docs |
| `docs/maintainers/` | Release, audit, CI drift, metadata maintenance docs |
| `docs/sources/` | Attribution and licensing references |
| `apps/web-app/` | Interactive browser for the skill catalog |
| `tools/` | Installer, validators, generators, and support scripts |
| `data/` | Generated catalog, aliases, bundles, and workflows |

## Top Starter Skills

- `@brainstorming` for planning before implementation.
- `@architecture` for system and component design.
- `@test-driven-development` for TDD-oriented work.
- `@doc-coauthoring` for structured documentation writing.
- `@lint-and-validate` for lightweight quality checks.
- `@create-pr` for packaging work into a clean pull request.
- `@debugging-strategies` for systematic troubleshooting.
- `@api-design-principles` for API shape and consistency.
- `@frontend-design` for UI and interaction quality.
- `@security-auditor` for security-focused reviews.

## Three Real Examples

```text
Use @brainstorming to turn this product idea into a concrete MVP plan.
```

```text
Use @security-auditor to review this API endpoint for auth and validation risks.
```

```text
Use @doc-coauthoring to rewrite our setup guide for first-time contributors.
```

## Browse 1,206+ Skills

- Open the interactive browser in [`apps/web-app`](apps/web-app).
- Read the full catalog in [`CATALOG.md`](CATALOG.md).
- Start with role-based bundles in [`docs/users/bundles.md`](docs/users/bundles.md).
- Follow outcome-driven workflows in [`docs/users/workflows.md`](docs/users/workflows.md).
- Use the onboarding guides in [`docs/users/getting-started.md`](docs/users/getting-started.md) and [`docs/users/usage.md`](docs/users/usage.md).

## Documentation

| For Users | For Contributors | For Maintainers |
| --- | --- | --- |
| [`docs/users/getting-started.md`](docs/users/getting-started.md) | [`CONTRIBUTING.md`](CONTRIBUTING.md) | [`docs/maintainers/release-process.md`](docs/maintainers/release-process.md) |
| [`docs/users/usage.md`](docs/users/usage.md) | [`docs/contributors/skill-anatomy.md`](docs/contributors/skill-anatomy.md) | [`docs/maintainers/audit.md`](docs/maintainers/audit.md) |
| [`docs/users/faq.md`](docs/users/faq.md) | [`docs/contributors/quality-bar.md`](docs/contributors/quality-bar.md) | [`docs/maintainers/ci-drift-fix.md`](docs/maintainers/ci-drift-fix.md) |
| [`docs/users/visual-guide.md`](docs/users/visual-guide.md) | [`docs/contributors/examples.md`](docs/contributors/examples.md) | [`docs/maintainers/skills-update-guide.md`](docs/maintainers/skills-update-guide.md) |

## Web App

The web app is the fastest way to navigate a large repository like this.

```bash
npm run app:install
npm run app:dev
```

That will copy the generated skill index into `apps/web-app/public/skills.json`, mirror the current `skills/` tree into `apps/web-app/public/skills/`, and start the Vite development server.

## Contributing

- Add new skills under `skills/<skill-name>/SKILL.md`.
- Follow the contributor guide in [`CONTRIBUTING.md`](CONTRIBUTING.md).
- Use the template in [`docs/contributors/skill-template.md`](docs/contributors/skill-template.md).
- Validate with `npm run validate` before opening a PR.

## Community

- [Discussions](https://github.com/sickn33/antigravity-awesome-skills/discussions) for questions and feedback.
- [Issues](https://github.com/sickn33/antigravity-awesome-skills/issues) for bugs and improvement requests.
- [`SECURITY.md`](SECURITY.md) for security reporting.

## Support the Project

Support is optional. The project stays free and open-source for everyone.

- [Buy me a book on Buy Me a Coffee](https://buymeacoffee.com/sickn33)
- Star the repository
- Open reproducible issues
- Contribute docs, fixes, and skills

---

## Credits & Sources

We stand on the shoulders of giants.

👉 **[View the Full Attribution Ledger](docs/sources/sources.md)**

Key contributors and sources include:

- **HackTricks**
- **OWASP**
- **Anthropic / OpenAI / Google**
- **The Open Source Community**

This collection would not be possible without the incredible work of the Claude Code community and official sources:

### Official Sources

- **[anthropics/skills](https://github.com/anthropics/skills)**: Official Anthropic skills repository - Document manipulation (DOCX, PDF, PPTX, XLSX), Brand Guidelines, Internal Communications.
- **[anthropics/claude-cookbooks](https://github.com/anthropics/claude-cookbooks)**: Official notebooks and recipes for building with Claude.
- **[remotion-dev/skills](https://github.com/remotion-dev/skills)**: Official Remotion skills - Video creation in React with 28 modular rules.
- **[vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills)**: Vercel Labs official skills - React Best Practices, Web Design Guidelines.
- **[openai/skills](https://github.com/openai/skills)**: OpenAI Codex skills catalog - Agent skills, Skill Creator, Concise Planning.
- **[supabase/agent-skills](https://github.com/supabase/agent-skills)**: Supabase official skills - Postgres Best Practices.
- **[microsoft/skills](https://github.com/microsoft/skills)**: Official Microsoft skills - Azure cloud services, Bot Framework, Cognitive Services, and enterprise development patterns across .NET, Python, TypeScript, Go, Rust, and Java.
- **[google-gemini/gemini-skills](https://github.com/google-gemini/gemini-skills)**: Official Gemini skills - Gemini API, SDK and model interactions.
- **[apify/agent-skills](https://github.com/apify/agent-skills)**: Official Apify skills - Web scraping, data extraction and automation.

### Community Contributors

- **[rmyndharis/antigravity-skills](https://github.com/rmyndharis/antigravity-skills)**: For the massive contribution of 300+ Enterprise skills and the catalog generation logic.
- **[amartelr/antigravity-workspace-manager](https://github.com/amartelr/antigravity-workspace-manager)**: Official Workspace Manager CLI companion to dynamically auto-provision subsets of skills across unlimited local development environments.
- **[obra/superpowers](https://github.com/obra/superpowers)**: The original "Superpowers" by Jesse Vincent.
- **[guanyang/antigravity-skills](https://github.com/guanyang/antigravity-skills)**: Core Antigravity extensions.
- **[diet103/claude-code-infrastructure-showcase](https://github.com/diet103/claude-code-infrastructure-showcase)**: Infrastructure and Backend/Frontend Guidelines.
- **[ChrisWiles/claude-code-showcase](https://github.com/ChrisWiles/claude-code-showcase)**: React UI patterns and Design Systems.
- **[travisvn/awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills)**: Loki Mode and Playwright integration.
- **[zebbern/claude-code-guide](https://github.com/zebbern/claude-code-guide)**: Comprehensive Security suite & Guide (Source for ~60 new skills).
- **[alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills)**: Senior Engineering and PM toolkit.
- **[karanb192/awesome-claude-skills](https://github.com/karanb192/awesome-claude-skills)**: A massive list of verified skills for Claude Code.
- **[VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills)**: Curated collection of 61 high-quality skills including official team skills from Sentry, Trail of Bits, Expo, Hugging Face, and comprehensive context engineering suite (v4.3.0 integration).
- **[zircote/.claude](https://github.com/zircote/.claude)**: Shopify development skill reference.
- **[vibeforge1111/vibeship-spawner-skills](https://github.com/vibeforge1111/vibeship-spawner-skills)**: AI Agents, Integrations, Maker Tools (57 skills, Apache 2.0).
- **[coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills)**: Marketing skills for CRO, copywriting, SEO, paid ads, and growth (23 skills, MIT).
- **[jonathimer/devmarketing-skills](https://github.com/jonathimer/devmarketing-skills)**: Developer marketing skills — HN strategy, technical tutorials, docs-as-marketing, Reddit engagement, developer onboarding, and more (33 skills, MIT).
- **[Silverov/yandex-direct-skill](https://github.com/Silverov/yandex-direct-skill)**: Yandex Direct (API v5) advertising audit skill — 55 automated checks, A-F scoring, campaign/ad/keyword analysis for the Russian PPC market (MIT).
- **[vudovn/antigravity-kit](https://github.com/vudovn/antigravity-kit)**: AI Agent templates with Skills, Agents, and Workflows (33 skills, MIT).
- **[affaan-m/everything-claude-code](https://github.com/affaan-m/everything-claude-code)**: Complete Claude Code configuration collection from Anthropic hackathon winner - skills only (8 skills, MIT).
- **[whatiskadudoing/fp-ts-skills](https://github.com/whatiskadudoing/fp-ts-skills)**: Practical fp-ts skills for TypeScript – fp-ts-pragmatic, fp-ts-react, fp-ts-errors (v4.4.0).
- **[webzler/agentMemory](https://github.com/webzler/agentMemory)**: Source for the agent-memory-mcp skill.
- **[sstklen/claude-api-cost-optimization](https://github.com/sstklen/claude-api-cost-optimization)**: Save 50-90% on Claude API costs with smart optimization strategies (MIT).
- **[Wittlesus/cursorrules-pro](https://github.com/Wittlesus/cursorrules-pro)**: Professional .cursorrules configurations for 8 frameworks - Next.js, React, Python, Go, Rust, and more. Works with Cursor, Claude Code, and Windsurf.
- **[nedcodes-ok/rule-porter](https://github.com/nedcodes-ok/rule-porter)**: Bidirectional rule converter between Cursor (.mdc), Claude Code (CLAUDE.md), GitHub Copilot, Windsurf, and legacy .cursorrules formats. Zero dependencies.
- **[SSOJet/skills](https://github.com/ssojet/skills)**: Production-ready SSOJet skills and integration guides for popular frameworks and platforms — Node.js, Next.js, React, Java, .NET Core, Go, iOS, Android, and more. Works seamlessly with SSOJet SAML, OIDC, and enterprise SSO flows. Works with Cursor, Antigravity, Claude Code, and Windsurf.
- **[MojoAuth/skills](https://github.com/MojoAuth/skills)**: Production-ready MojoAuth guides and examples for popular frameworks like Node.js, Next.js, React, Java, .NET Core, Go, iOS, and Android.
- **[Xquik-dev/x-twitter-scraper](https://github.com/Xquik-dev/x-twitter-scraper)**: X (Twitter) data platform — tweet search, user lookup, follower extraction, engagement metrics, giveaway draws, monitoring, webhooks, 19 extraction tools, MCP server.
- **[shmlkv/dna-claude-analysis](https://github.com/shmlkv/dna-claude-analysis)**: Personal genome analysis toolkit — Python scripts analyzing raw DNA data across 17 categories (health risks, ancestry, pharmacogenomics, nutrition, psychology, etc.) with terminal-style single-page HTML visualization.

### Inspirations

- **[f/awesome-chatgpt-prompts](https://github.com/f/awesome-chatgpt-prompts)**: Inspiration for the Prompt Library.
- **[leonardomso/33-js-concepts](https://github.com/leonardomso/33-js-concepts)**: Inspiration for JavaScript Mastery.

### Additional Sources

- **[agent-cards/skill](https://github.com/agent-cards/skill)**: Manage prepaid virtual Visa cards for AI agents. Create cards, check balances, view credentials, close cards, and get support via MCP tools.

## Repo Contributors

<a href="https://github.com/sickn33/antigravity-awesome-skills/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=sickn33/antigravity-awesome-skills" alt="Repository contributors" />
</a>

Made with [contrib.rocks](https://contrib.rocks).

We officially thank the following contributors for their help in making this repository awesome!

- [@sickn33](https://github.com/sickn33)
- [@munir-abbasi](https://github.com/munir-abbasi)
- [@ssumanbiswas](https://github.com/ssumanbiswas)
- [@zinzied](https://github.com/zinzied)
- [@Mohammad-Faiz-Cloud-Engineer](https://github.com/Mohammad-Faiz-Cloud-Engineer)
- [@Dokhacgiakhoa](https://github.com/Dokhacgiakhoa)
- [@IanJ332](https://github.com/IanJ332)
- [@chauey](https://github.com/chauey)
- [@ar27111994](https://github.com/ar27111994)
- [@8hrsk](https://github.com/8hrsk)
- [@itsmeares](https://github.com/itsmeares)
- [@GuppyTheCat](https://github.com/GuppyTheCat)
- [@fernandorych](https://github.com/fernandorych)
- [@nikolasdehor](https://github.com/nikolasdehor)
- [@talesperito](https://github.com/talesperito)
- [@jackjin1997](https://github.com/jackjin1997)
- [@HuynhNhatKhanh](https://github.com/HuynhNhatKhanh)
- [@liyin2015](https://github.com/liyin2015)
- [@arathiesh](https://github.com/arathiesh)
- [@Tiger-Foxx](https://github.com/Tiger-Foxx)
- [@Musayrlsms](https://github.com/Musayrlsms)
- [@sohamganatra](https://github.com/sohamganatra)
- [@SuperJMN](https://github.com/SuperJMN)
- [@SebConejo](https://github.com/SebConejo)
- [@Onsraa](https://github.com/Onsraa)
- [@truongnmt](https://github.com/truongnmt)
- [@code-vj](https://github.com/code-vj)
- [@viktor-ferenczi](https://github.com/viktor-ferenczi)
- [@vprudnikoff](https://github.com/vprudnikoff)
- [@Vonfry](https://github.com/Vonfry)
- [@Wittlesus](https://github.com/Wittlesus)
- [@avimak](https://github.com/avimak)
- [@buzzbysolcex](https://github.com/buzzbysolcex)
- [@c1c3ru](https://github.com/c1c3ru)
- [@ckdwns9121](https://github.com/ckdwns9121)
- [@developer-victor](https://github.com/developer-victor)
- [@fbientrigo](https://github.com/fbientrigo)
- [@junited31](https://github.com/junited31)
- [@KrisnaSantosa15](https://github.com/KrisnaSantosa15)
- [@nocodemf](https://github.com/nocodemf)
- [@sstklen](https://github.com/sstklen)
- [@taksrules](https://github.com/taksrules)
- [@thuanlm215](https://github.com/thuanlm215)
- [@zebbern](https://github.com/zebbern)
- [@vuth-dogo](https://github.com/vuth-dogo)
- [@ALEKGG1](https://github.com/ALEKGG1)
- [@Abdulrahmansoliman](https://github.com/Abdulrahmansoliman)
- [@alexmvie](https://github.com/alexmvie)
- [@Andruia](https://github.com/Andruia)
- [@acbhatt12](https://github.com/acbhatt12)
- [@BenedictKing](https://github.com/BenedictKing)
- [@rcigor](https://github.com/rcigor)
- [@whatiskadudoing](https://github.com/whatiskadudoing)
- [@k-kolomeitsev](https://github.com/k-kolomeitsev)
- [@Krishna-Modi12](https://github.com/Krishna-Modi12)
- [@kromahlusenii-ops](https://github.com/kromahlusenii-ops)
- [@djmahe4](https://github.com/djmahe4)
- [@maxdml](https://github.com/maxdml)
- [@mertbaskurt](https://github.com/mertbaskurt)
- [@nedcodes-ok](https://github.com/nedcodes-ok)
- [@LocNguyenSGU](https://github.com/LocNguyenSGU)
- [@KhaiTrang1995](https://github.com/KhaiTrang1995)
- [@sharmanilay](https://github.com/sharmanilay)
- [@yubing744](https://github.com/yubing744)
- [@PabloASMD](https://github.com/PabloASMD)
- [@0xrohitgarg](https://github.com/0xrohitgarg)
- [@Silverov](https://github.com/Silverov)
- [@shmlkv](https://github.com/shmlkv)
- [@kriptoburak](https://github.com/kriptoburak)
- [@lsuryatej](https://github.com/lsuryatej)
- [@tejasashinde](https://github.com/tejasashinde)
- [@SnakeEye-sudo](https://github.com/SnakeEye-sudo)
- [@8144225309](https://github.com/8144225309)
- [@RamonRiosJr](https://github.com/RamonRiosJr)
- [@sx4im](https://github.com/sx4im)
- [@skyruh](https://github.com/skyruh)
- [@nagisanzenin](https://github.com/nagisanzenin)
- [@devchangjun](https://github.com/devchangjun)
- [@raeef1001](https://github.com/raeef1001)
- [@1bcMax](https://github.com/1bcMax)

---

## License

MIT License. See [LICENSE](LICENSE) for details.

---

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=sickn33/antigravity-awesome-skills&type=date&legend=top-left)](https://www.star-history.com/#sickn33/antigravity-awesome-skills&type=date&legend=top-left)

If Antigravity Awesome Skills has been useful, consider ⭐ starring the repo!

<!-- GitHub Topics (for maintainers): claude-code, gemini-cli, codex-cli, antigravity, cursor, github-copilot, opencode, agentic-skills, ai-coding, llm-tools, ai-agents, autonomous-coding, mcp, ai-developer-tools, ai-pair-programming, vibe-coding, skill, skills, SKILL.md, rules.md, CLAUDE.md, GEMINI.md, CURSOR.md -->
