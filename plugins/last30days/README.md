# last30days

Vendored Codex plugin wrapper for [mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill).

This repo carries the upstream runtime scripts plus a Codex-native plugin manifest and marketplace metadata. The main skill entrypoint is [skills/last30days/SKILL.md](./skills/last30days/SKILL.md).

Runtime requirements:

- Python 3.12+
- `requests`
- Optional: `yt-dlp` for YouTube
- Optional keys/tokens for richer sources: `SCRAPECREATORS_API_KEY`, `BRAVE_API_KEY` or `SERPER_API_KEY`, `XAI_API_KEY`, `AUTH_TOKEN` + `CT0`

Project-local config files are checked in this order:

1. `.codex/last30days.env`
2. `.claude/last30days.env`
3. `~/.config/last30days/.env`
