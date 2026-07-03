# Obsidian Vault Sync

This workstation uses two Obsidian vaults:

- `C:\works`: primary work vault.
- `C:\design`: design reference vault.

Both vaults are local Git repositories on this PC.

Current local baselines:

- `C:\works`: `bc217ba` (`Add works Obsidian vault baseline`)
- `C:\design`: `02bbf03` (`Add design Obsidian vault baseline`)

## GitHub Target

Use private repositories:

- `works`
- `design`

Clone them into the exact paths on a new Windows PC:

```powershell
git clone <private-works-repo-url> C:\works
git clone <private-design-repo-url> C:\design
```

## What Is Included

Included:

- Markdown notes
- project folders
- non-secret Obsidian settings
- scripts and non-secret working docs
- selected project deliverables that are part of the vault

Excluded by `.gitignore`:

- logs
- temp folders
- browser profile captures
- token/key/credential/auth files
- SQLite and DB runtime files
- JSONL runtime/session files
- Obsidian `workspace.json`

## Operating Rule

Use GitHub as the sync and version-history layer. Use Notion as the readable runbook and link hub. Do not treat Notion as the source of truth for exact file contents.
