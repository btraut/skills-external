# Codex / Claude Agent Skills (External)

Home for external skills and plugins used by Codex CLI and Claude-based agents. The repo is split cleanly: skills live under `skills/`, plugins live under `plugins/`.

## What's inside
Best-effort source mapping is included so it is obvious where each imported skill came from.

### Skills

| Skill | What it does | Source |
| --- | --- | --- |
| `skills/agent-browser/` | Browser automation CLI workflows for opening pages, clicking, filling forms, extracting data, and testing web apps. | [openclaw/skills](https://github.com/openclaw/skills) |
| `skills/babysit-pr/` | Monitor a GitHub PR until it is mergeable, handling CI failures, flaky retries, and review feedback along the way. | [openai/codex](https://github.com/openai/codex) |
| `skills/beads-rust/` | Local-first issue tracking for multi-session work with dependencies, ready-queue triage, and explicit JSONL sync via `br`. | [Dicklesworthstone/beads_rust/.claude/skills/br](https://github.com/Dicklesworthstone/beads_rust/tree/main/.claude/skills/br) |
| `skills/code-review-excellence/` | Code review guidance focused on finding real problems without turning review into performative bullshit. | [wshobson/agents](https://github.com/wshobson/agents) |
| `skills/context7/` | Fetch current third-party library documentation instead of guessing outdated APIs. | [openclaw/skills](https://github.com/openclaw/skills) |
| `skills/de-slopify/` | Remove AI writing tells from READMEs and docs through manual line-by-line editing. | [Dicklesworthstone/agent_flywheel_clawdbot_skills_and_integrations](https://github.com/Dicklesworthstone/agent_flywheel_clawdbot_skills_and_integrations/tree/main/skills/de-slopify) |
| `skills/frontend-design/` | Create distinctive, production-grade frontend interfaces with high design quality. | [anthropics/skills](https://github.com/anthropics/skills/tree/main/skills/frontend-design) |
| `skills/railway-cli/` | Deploy and manage Railway services, env vars, logs, volumes, and service operations. | [CaptainCrouton89/.claude](https://github.com/CaptainCrouton89/.claude/tree/main/skills.archive/railway-cli) |
| `skills/rclone/` | Upload, sync, and manage files across S3-compatible and other cloud storage providers. | [everyinc/compound-engineering-plugin](https://github.com/everyinc/compound-engineering-plugin) |
| `skills/react-useeffect/` | React `useEffect` best practices, especially when not to use it. | [davila7/claude-code-templates](https://github.com/davila7/claude-code-templates) |
| `skills/read-github/` | Read and search GitHub repository docs and code through gitmcp.io. | [am-will/codex-skills](https://github.com/am-will/codex-skills) |
| `skills/tailwind-design-system/` | Design-system patterns for Tailwind CSS v4, tokens, components, and responsive UI. | [wshobson/agents](https://github.com/wshobson/agents) |

### Plugins

| Plugin | What it does | Source |
| --- | --- | --- |
| `plugins/last30days/` | Codex-native wrapper for the `last30days` research workflow, pulling recent signal from Reddit, X, YouTube, TikTok, Instagram, Hacker News, Polymarket, GitHub, and grounded web search. | [mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill) |

## Installing these skills

```bash
npx skills add btraut/skills-external
```

Fallback: clone this repo locally, then copy or symlink the directories under `skills/` into your agent's skills directory, such as `$CODEX_HOME/skills`.

## Installing the included Codex plugin

The bundled `last30days` plugin uses Codex's local marketplace layout:

- plugin source: `plugins/last30days/`
- marketplace file: `.agents/plugins/marketplace.json`

Safe install flow:

1. Clone this repo locally.
2. Point Codex at the repo-local marketplace file, or copy the `last30days` entry into `~/.agents/plugins/marketplace.json`.
3. Install the `last30days` plugin from that marketplace entry.

The vendored plugin checks project-local config in `.codex/last30days.env` first, then `.claude/last30days.env`, then `~/.config/last30days/.env`.

## Changelog
See [CHANGELOG.md](CHANGELOG.md).
