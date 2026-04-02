# br Troubleshooting

## Doctor

```bash
br doctor
```

This checks database integrity, sync status, config validity, and path permissions.

## Common Fixes

### Database Locked

```bash
pgrep -f "br "
br sync --status
```

### Issue Not Found

```bash
br list --json | jq '.issues[] | select(.id == "<id>")'
br search "keyword" --json
```

### Prefix Mismatch

```bash
br config get id.prefix
br sync --import-only --skip-prefix-validation
```

### Worktree Error

If you hit `failed to create worktree: 'main' is already checked out`:

```bash
git branch beads-sync main
git push -u origin beads-sync
br config set sync.branch beads-sync
```

### Sync Weirdness After Merge

```bash
git status .beads/
br sync --import-only
br doctor
```

## Debugging

```bash
br -v list
br -vv list
RUST_LOG=debug br list
```

## Quick Health Check

```bash
br doctor
br dep cycles
br config list
which br
br version
```
