# Codex / Claude Agent Skills (External)

Home for external skills used by Codex CLI and Claude-based agents. These are the shared skills that live outside the main `skills` repo but still belong in the same install flow.

## What's inside
Best-effort source mapping is included so it is obvious where each imported skill came from.

| Skill | What it does | Source |
| --- | --- | --- |
| `agent-browser/` | Browser automation CLI workflows for opening pages, clicking, filling forms, extracting data, and testing web apps. | [openclaw/skills](https://github.com/openclaw/skills) |
| `babysit-pr/` | Monitor a GitHub PR until it is mergeable, handling CI failures, flaky retries, and review feedback along the way. | [openai/codex](https://github.com/openai/codex) |
| `beads-rust/` | Local-first issue tracking for multi-session work with dependencies, ready-queue triage, and explicit JSONL sync via `br`. | [Dicklesworthstone/beads_rust/.claude/skills/br](https://github.com/Dicklesworthstone/beads_rust/tree/main/.claude/skills/br) |
| `code-review-excellence/` | Code review guidance focused on finding real problems without turning review into performative bullshit. | [wshobson/agents](https://github.com/wshobson/agents) |
| `context7/` | Fetch current third-party library documentation instead of guessing outdated APIs. | [openclaw/skills](https://github.com/openclaw/skills) |
| `de-slopify/` | Remove AI writing tells from READMEs and docs through manual line-by-line editing. | [Dicklesworthstone/agent_flywheel_clawdbot_skills_and_integrations](https://github.com/Dicklesworthstone/agent_flywheel_clawdbot_skills_and_integrations/tree/main/skills/de-slopify) |
| `frontend-design/` | Create distinctive, production-grade frontend interfaces with high design quality. | [anthropics/skills](https://github.com/anthropics/skills/tree/main/skills/frontend-design) |
| `railway-cli/` | Deploy and manage Railway services, env vars, logs, volumes, and service operations. | [CaptainCrouton89/.claude](https://github.com/CaptainCrouton89/.claude/tree/main/skills.archive/railway-cli) |
| `rclone/` | Upload, sync, and manage files across S3-compatible and other cloud storage providers. | [everyinc/compound-engineering-plugin](https://github.com/everyinc/compound-engineering-plugin) |
| `react-useeffect/` | React `useEffect` best practices, especially when not to use it. | [davila7/claude-code-templates](https://github.com/davila7/claude-code-templates) |
| `read-github/` | Read and search GitHub repository docs and code through gitmcp.io. | [am-will/codex-skills](https://github.com/am-will/codex-skills) |
| `tailwind-design-system/` | Design-system patterns for Tailwind CSS v4, tokens, components, and responsive UI. | [wshobson/agents](https://github.com/wshobson/agents) |

## Installing these skills

```bash
npx skills add btraut/skills-external
```

Fallback: clone or place this repo in your agent's skills directory, such as `$CODEX_HOME/skills`.

## Changelog
See [CHANGELOG.md](CHANGELOG.md).
