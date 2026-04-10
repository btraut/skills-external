---
name: beads-rust
description: >
  Official skill for beads_rust (`br`), a local-first, dependency-aware issue
  tracker for AI agents. Use when creating issues, triaging backlogs, managing
  dependencies, finding ready work, updating status, or syncing issue state to
  git via JSONL.
---

# Beads Rust Issue Tracker

> `br` never runs git commands for you. Syncing `.beads/` and committing it is your job.

## Critical Rules

| Rule | Why |
|------|-----|
| Use `br`, never `bd` | `bd` is the old Go-based tool |
| Use `--json` for agent reads | Structured output is easier to parse and reason about |
| Never run bare `bv` | It opens an interactive TUI and blocks the session |
| Keep sync explicit | Use `br sync --flush-only` before git commits and `br sync --import-only` after pulls |
| Keep the graph acyclic | `br dep cycles --json` must be empty |
| Resolve actor at runtime | `ACTOR="${BR_ACTOR:-assistant}"`, then pass `--actor "$ACTOR"` on mutating commands |

## Quick Workflow

```bash
ACTOR="${BR_ACTOR:-assistant}"

# 1. Find ready work
br ready --json

# 2. Claim it
br update --actor "$ACTOR" <id> --status in_progress --claim

# 3. Do the work...

# 4. Close it with evidence
br close --actor "$ACTOR" <id> --reason "Implemented X"

# 5. Export issue state before committing
br sync --flush-only
git add .beads/ && git commit -m "feat: X (<id>)"
```

## Essential Commands

### Issue Lifecycle

```bash
ACTOR="${BR_ACTOR:-assistant}"

br init                                              # Initialize .beads/ workspace
br create --actor "$ACTOR" "Title" -p 1 -t task      # Create issue (priority 0-4)
br q --actor "$ACTOR" "Quick note"                   # Quick capture (returns ID)
br show <id> --json                                  # Show issue details
br update --actor "$ACTOR" <id> --status in_progress # Update status
br update --actor "$ACTOR" <id> --priority 0         # Change priority
br close --actor "$ACTOR" <id> --reason "Done"       # Close with reason
br close --actor "$ACTOR" <id1> <id2> --reason "..." # Close multiple issues
br reopen --actor "$ACTOR" <id>                      # Reopen closed issue
```

### Create and Update Options

```bash
br create --actor "$ACTOR" "Title" \
  --priority 1 \
  --type task \
  --assignee "user@..." \
  --labels backend,auth \
  --description "..."

br update --actor "$ACTOR" <id> \
  --title "New title" \
  --priority 0 \
  --status in_progress \
  --assignee "new@..." \
  --add-label reliability \
  --parent <parent-id> \
  --claim
```

Bulk triage:

```bash
br update --actor "$ACTOR" <id1> <id2> <id3> --priority 2 --add-label triage-reviewed --json
```

### Querying

```bash
br ready --json
br list --json
br list --status open --sort priority --json
br list --priority 0-1 --json
br list --assignee alice --json
br blocked --json
br search "keyword" --json
br show <id> --json
br stale --days 30 --json
br count --by status --json
```

### Dependencies

```bash
br dep add <child> <parent>
br dep add <id> <depends-on> --type blocks
br dep remove <child> <parent>
br dep list <id> --json
br dep tree <id> --json
br dep cycles --json
```

`br dep cycles --json` must return no cycles. If the graph is cyclic, `br ready` becomes untrustworthy.

### Labels, Comments, and Sync

```bash
br label add <id> backend auth
br label remove <id> urgent
br label list <id>
br label list-all

br comments add --actor "$ACTOR" <id> --message "Triage note" --json
br comments list <id> --json

br sync --flush-only
br sync --import-only
br sync --status
```

### Diagnostics

```bash
br doctor
br stats --json
br config list
br config get id.prefix
br config set defaults.priority=1
br where
br version
br upgrade
br lint --json
```

## Priority Scale

| Priority | Meaning |
|----------|---------|
| 0 | Critical |
| 1 | High |
| 2 | Medium (default) |
| 3 | Low |
| 4 | Backlog |

## Output Formats

| Flag | Use case |
|------|----------|
| `--json` | Default for agents |
| `--format toon` | Lower-token alternative when context is tight |
| No flag | Human terminal output |

## `bv` Integration

Never run bare `bv`.

```bash
bv --robot-next
bv --robot-triage
bv --robot-plan
bv --robot-insights | jq '.Cycles'
bv --robot-priority
bv --robot-alerts
```

## Agent Coordination

Use the bead ID as the shared coordination key when multiple agents touch the same work item.

- Reuse the issue ID in subagent prompts, progress updates, and commit messages.
- If your runtime supports file reservations or agent messaging, use the bead ID as the reservation reason or thread key.
- If you cannot prove an issue is done, add a comment with what is missing instead of closing it.

## Standard Session Pattern

```bash
ACTOR="${BR_ACTOR:-assistant}"

br where
br ready --json
br blocked --json
br list --status open --sort priority --json
br show <id> --json
br update --actor "$ACTOR" <id> --status in_progress --claim
# Do work...
br close --actor "$ACTOR" <id> --reason "Implemented X in commit abc123"
br ready --json
br blocked --json
br sync --flush-only
git add .beads/ && git commit -m "feat: X (<id>)"
git push
```

Before ending a session:

```bash
git pull --rebase
br sync --flush-only
git add .beads/ && git commit -m "Update issues"
git push
git status
```

## Anti-Patterns

- Running `br sync` without `--flush-only` or `--import-only`
- Forgetting to sync before committing `.beads/`
- Creating circular dependencies
- Running bare `bv`
- Pretending `br` auto-commits or auto-pushes
- Closing issues without evidence
- Editing unrelated issues during triage

## Storage Layout

```text
.beads/
  beads.db
  beads.db-shm
  beads.db-wal
  issues.jsonl
  config.yaml
  metadata.json
```

## References

| Topic | File |
|-------|------|
| Command cookbook | [references/COMMANDS.md](references/COMMANDS.md) |
| Configuration details | [references/CONFIG.md](references/CONFIG.md) |
| Troubleshooting guide | [references/TROUBLESHOOTING.md](references/TROUBLESHOOTING.md) |
| Agent integration patterns | [references/INTEGRATION.md](references/INTEGRATION.md) |
