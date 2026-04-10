# Changelog

- 2026-04-10: Added a new `plugins/` tree with a repo-local Codex marketplace file, then vendored `plugins/last30days/` from [mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill) with a Codex plugin manifest, marketplace entry, and small config/path tweaks for `.codex/last30days.env` support.
- 2026-04-01: Replaced the old `beads/` skill with `beads-rust/`, imported the upstream `br` skill and reference docs from [Dicklesworthstone/beads_rust/.claude/skills/br](https://github.com/Dicklesworthstone/beads_rust/tree/main/.claude/skills/br), and rewrote the Claude-only coordination guidance for Codex.
- 2026-03-21: Replaced `frontend-design-ultimate/` with Anthropic's official `frontend-design/` skill from [anthropics/skills](https://github.com/anthropics/skills/tree/main/skills/frontend-design).
- 2026-03-15: Added `de-slopify/` from [Dicklesworthstone/agent_flywheel_clawdbot_skills_and_integrations](https://github.com/Dicklesworthstone/agent_flywheel_clawdbot_skills_and_integrations/tree/main/skills/de-slopify).
- 2026-03-09: README now uses `npx skills add btraut/skills-external` as the primary install flow and mirrors the sibling `skills` repo format.
- 2026-03-09: Added a root `AGENTS.md` rule requiring README and changelog updates whenever a skill is added, removed, or modified.
- 2026-03-09: Added best-effort upstream source links for imported skills and required future skill additions to record their source in `AGENTS.md`.
- 2026-03-09: Identified `babysit-pr` as coming from `openai/codex` and updated the source mapping.
