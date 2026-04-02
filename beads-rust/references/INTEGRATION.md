# br Integration Patterns

## `bv` Integration

`bv` is the graph-aware viewer and triage tool for beads_rust.

Never run bare `bv`.

```bash
bv --robot-triage
bv --robot-next
bv --robot-plan
bv --robot-insights
bv --robot-priority
bv --robot-alerts
bv --robot-suggest
```

### Check Graph Health

```bash
bv --robot-insights | jq '.Cycles'
bv --robot-insights | jq '.bottlenecks'
```

### Scoped Planning

```bash
bv --robot-plan --label backend
bv --robot-insights --as-of HEAD~30
bv --recipe actionable --robot-plan
bv --recipe high-impact --robot-triage
```

## Multi-Agent Coordination

Use the bead ID as the shared handle for coordination.

- Reuse `<id>` in subagent prompts so everyone is talking about the same issue.
- Reuse `<id>` in progress updates, temporary notes, and commit messages.
- If your runtime supports file reservations or messaging, use `<id>` as the reservation reason or thread key.
- Close the bead only after the work and its evidence exist.

### Standard Agent Workflow

```bash
ACTOR="${BR_ACTOR:-assistant}"

br ready --json
br update --actor "$ACTOR" <id> --status in_progress --claim
# Reserve or communicate ownership using <id> if your runtime supports it
# Do work...
br close --actor "$ACTOR" <id> --reason "Implemented feature X"
br sync --flush-only
git add .beads/
git commit -m "feat: implement X (<id>)"
```

## Creating Good Issues

```bash
ACTOR="${BR_ACTOR:-assistant}"

br create --actor "$ACTOR" "Title that explains the task" \
  --type task \
  --priority 1 \
  --description "Detailed description with acceptance criteria"
```

Good issue descriptions include:

- Clear scope
- Acceptance criteria
- Real dependencies added with `br dep add`
- Enough context for a future agent with zero memory

## Differences from `bd`

| Aspect | `br` | `bd` |
|--------|------|------|
| Git operations | Explicit sync only | More automatic |
| Storage | SQLite + JSONL | Dolt/SQLite |
| Background daemon | No | Yes |
| Hook installation | Manual | More automatic |
| Complexity | Focused | Broader |

`br` does not do automatic commits, hook installation, background daemons, or Dolt sync. That's deliberate, not a missing checkbox.
