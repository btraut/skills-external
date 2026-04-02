# br Configuration

## Precedence

1. CLI flags
2. Environment variables
3. Project config: `.beads/config.yaml`
4. User config: `~/.config/beads/config.yaml`
5. Defaults

## Example Config

```yaml
# .beads/config.yaml

id:
  prefix: "myproject"

defaults:
  priority: 2
  type: "task"
  assignee: "team@example.com"

output:
  color: true
  date_format: "%Y-%m-%d"

sync:
  auto_import: false
  auto_flush: false
  branch: beads-sync
```

## Environment Variables

| Variable | Description |
|----------|-------------|
| `BR_ACTOR` | Default actor identity |
| `BEADS_DB` | Override database path |
| `BEADS_JSONL` | Override JSONL path |
| `RUST_LOG` | Logging level |

## Config Commands

```bash
br config list
br config get id.prefix
br config set defaults.priority=1
```

## Storage Paths

```text
.beads/
  beads.db
  beads.db-shm
  beads.db-wal
  issues.jsonl
  config.yaml
  metadata.json
```
