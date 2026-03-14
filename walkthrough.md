# Maintenance Walkthrough - 2026-03-12

- Merged PRs `#277`, `#272`, `#275`, `#278`, and `#271` via GitHub squash merge after bringing contributor branches into a mergeable state and refreshing PR bodies against the quality checklist in `.github/MAINTENANCE.md`.
- Verified PR `#271` locally with `npm run validate:references` and `npm run test` before merge; confirmed `#269` auto-closed from the merged PR body.
- Added a user-facing Windows truncation recovery guide at `docs/users/windows-truncation-recovery.md`, linked it from `README.md`, `docs/users/faq.md`, `docs/users/getting-started.md`, and `docs/integrations/jetski-cortex.md`, and credited the workflow to issue `#274`.
- Updated `skills/metasploit-framework/SKILL.md` to remove the remote installer flow, require an existing Metasploit installation, and add the required offensive-skill warning.
- Refreshed `README.md` to remove stale `7.2.0` / `7.4.0` onboarding copy, align the star badge with the current milestone, and fix the TOC link for `## Contributing`.
- Normalized the active English docs (`README.md`, user guides, Kiro guide, and evergreen maintainer docs) to the current `7.6.0` / `1,250+ skills` state and removed emoji from H2 headers where maintenance rules require clean anchors.
- Ran the required maintenance validations after the direct fixes:
  - `npm run validate`
  - `npm run validate:references`
  - `npm run chain`
  - `npm run catalog`
- Final release prep, issue closure comments, and verification were completed on `main`.

# Maintenance Walkthrough - 2026-03-13

- Fixed `tools/scripts/update_readme.py` so normal `npm run readme` runs preserve the existing `registry-sync` star/timestamp values instead of rewriting them on every execution, which was causing non-deterministic PR drift failures in CI.
- Updated `tools/scripts/sync_repo_metadata.py` to expose the same explicit `--refresh-volatile` behavior for live star/timestamp refreshes, keeping release/metadata refresh flows available without destabilizing contributor PR checks.
- Updated `.github/workflows/ci.yml` so generated registry drift is informational on pull requests but still strict on `main`, with auto-sync remaining the canonical path for shared artifacts after merge.
- Updated `.github/MAINTENANCE.md`, `docs/maintainers/ci-drift-fix.md`, and `docs/maintainers/merging-prs.md` to document the lower-friction merge flow: validate source changes on PRs, keep `main` for generated conflicts, and let `main` auto-sync the final artifact set.
- Verified the fix with:
  - `python3 tools/scripts/update_readme.py --dry-run`
  - `python3 tools/scripts/sync_repo_metadata.py --dry-run`
  - `npm run readme`
  - `npm run validate:references`
- Added `tools/config/generated-files.json` as the single contract for derived registry artifacts so CI, maintainer scripts, and docs share the same file list.
- Added scripted workflow entrypoints: `npm run pr:preflight`, `npm run release:preflight`, `npm run release:prepare -- X.Y.Z`, and `npm run release:publish -- X.Y.Z`.
- Split PR CI into `pr-policy`, `source-validation`, and `artifact-preview` so PRs stay source-only, policy failures are explicit, and generated drift is previewed separately from source validation.
- Updated `CONTRIBUTING.md` and `.github/PULL_REQUEST_TEMPLATE.md` so contributors are told not to commit derived files and to enable `Allow edits from maintainers`.

# Maintenance Walkthrough - 2026-03-14

- Added root Claude Code plugin marketplace support via `.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json`, exposing the repository as a single plugin entry that points at the existing `skills/` tree.
- Updated the user onboarding trinity (`README.md`, `docs/users/getting-started.md`, `docs/users/faq.md`) so Claude Code users can install via `/plugin marketplace add sickn33/antigravity-awesome-skills` in addition to the existing `npx` installer flow.
