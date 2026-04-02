# br Command Reference

## Global Flags

| Flag | Description |
|------|-------------|
| `--json` | JSON output for agents |
| `--format toon` | Token-optimized output |
| `--quiet` / `-q` | Suppress output |
| `--verbose` / `-v` | Increase verbosity (`-vv` for debug) |
| `--no-color` | Disable colored output |
| `--db <path>` | Override database path |
| `--actor <name>` | Set actor for audit trail |
| `--lock-timeout <ms>` | SQLite busy timeout |
| `--no-db` | JSONL-only mode |
| `--allow-stale` | Bypass freshness check |
| `--no-auto-flush` | Skip auto-export after mutations |
| `--no-auto-import` | Skip auto-import before reads |

## Actor Resolution

```bash
ACTOR="${BR_ACTOR:-assistant}"
```

Pass `--actor "$ACTOR"` on mutating commands.

## Issue Lifecycle

```bash
ACTOR="${BR_ACTOR:-assistant}"

br init
br create --actor "$ACTOR" "Title" -p 1 --type bug
br q --actor "$ACTOR" "Quick note"
br show <id> --json
br update --actor "$ACTOR" <id> --priority 0
br close --actor "$ACTOR" <id> --reason "Done"
br close --actor "$ACTOR" <id> --reason "..." --suggest-next --json
br close --actor "$ACTOR" <id> --reason "..." --force --json
br reopen --actor "$ACTOR" <id> --reason "..."
br delete <id>
```

### Create Options

```bash
br create --actor "$ACTOR" "Title" \
  --priority 1 \
  --type task \
  --assignee "user@..." \
  --labels backend,auth \
  --description "..."
```

### Update Options

```bash
br update --actor "$ACTOR" <id> \
  --title "New title" \
  --priority 0 \
  --status in_progress \
  --assignee "new@..." \
  --add-label reliability \
  --parent <parent-id> \
  --claim
```

### Bulk Update

```bash
br update --actor "$ACTOR" <id1> <id2> <id3> --priority 2 --add-label triage-reviewed --json
```

## Querying

```bash
br list --json
br list --status open --json
br list --status open --sort priority --json
br list --priority 0-1 --json
br list --assignee alice --json
br ready --json
br blocked --json
br search "authentication" --json
br show <id> --json
br stale --days 30 --json
br count --by status --json
br stats --json
br lint --json
```

## Dependencies

```bash
br dep add <child> <parent>
br dep add <id> <depends-on> --type blocks
br dep remove <child> <parent>
br dep list <id> --json
br dep tree <id> --json
br dep cycles --json
```

## Labels

```bash
br label add <id> backend auth
br label remove <id> urgent
br label list <id>
br label list-all
```

## Comments

```bash
ACTOR="${BR_ACTOR:-assistant}"
br comments add --actor "$ACTOR" <id> --message "Triage note" --json
br comments list <id> --json
```

## Sync

```bash
br sync --flush-only
br sync --import-only
br sync --status
```

## System

```bash
br doctor
br where
br config list
br config get id.prefix
br config set defaults.priority=1
br version
br upgrade
```

## JSON Output Examples

```bash
br ready --json | jq '.[0]'
br list --json | jq '.issues[] | select(.priority <= 1)'
br show <id> --json | jq '.[0].title'
br list --status open --json | jq '.issues | group_by(.type) | map({type: .[0].type, count: length})'
```
