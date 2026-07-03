# OpenClaw Agent Sync

Do not sync the raw `%USERPROFILE%\.openclaw\agents` folder directly.

The raw folder is large and contains runtime data:

- sessions
- logs
- SQLite state
- plugin caches
- temporary plugin folders
- auth-adjacent files
- generated run artifacts

This repo stores only the safe pieces needed to reproduce the worker setup:

- `openclaw/agents.current.safe.json`
- `openclaw/agent-instructions/<agent-id>/AGENTS.md`
- `openclaw/worker-layout.md`
- `openclaw/agents.example.json`
- `openclaw/models.example.json`

## Restore Flow

1. Install OpenClaw on the new PC.
2. Complete Codex/OpenAI login on that PC.
3. Add the Gemini API key on that PC.
4. Recreate the agent list from `agents.current.safe.json`.
5. Copy each `AGENTS.md` into:

```text
%USERPROFILE%\.openclaw\agents\<agent-id>\agent\AGENTS.md
```

6. Restart OpenClaw Gateway.
7. Validate with:

```powershell
openclaw config validate
openclaw health
openclaw agents list
openclaw models status
```

## Current Policy

- Codex/OpenAI remains the high-quality work lane.
- Gemini is not automatic text fallback.
- Gemini is image/visual asset support through image agents.
- Builder agents do not own design direction or image generation.
