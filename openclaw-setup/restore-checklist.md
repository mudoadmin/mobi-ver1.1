# Restore Checklist

Use this checklist when setting up another computer.

## 1. Install Base Tools

- Windows PowerShell
- Node.js
- OpenClaw CLI
- Git
- Obsidian
- PowerPoint desktop app if PPTX COM validation/export is needed
- Optional: Ollama, only if local models will actually be used

## 2. Initialize OpenClaw

```powershell
openclaw setup
openclaw configure
openclaw gateway install
openclaw gateway start
openclaw status
```

Expected:

```text
ws://127.0.0.1:18789
http://127.0.0.1:18789/
```

## 3. Enable Plugins

Required:

- `codex`
- `openai`
- `google`
- `telegram`
- `browser`
- `duckduckgo`
- `web-readability`
- `memory-core`

Optional:

- `ollama`

## 4. Authenticate Codex/OpenAI

Use OpenClaw guided auth. Do not copy tokens from another PC.

```powershell
openclaw models auth add
openclaw models auth list
openclaw models status
```

Expected policy:

- default text model: `openai/gpt-5.5`
- text fallbacks: none

## 5. Authenticate Gemini

Use Gemini only for image lanes.

```powershell
openclaw models auth paste-api-key --provider google --profile-id google:default
openclaw infer model run --local --model google/gemini-3-flash-preview --prompt "Reply with exactly: GEMINI_OK"
```

Expected:

```text
GEMINI_OK
```

## 6. Configure Models

```powershell
openclaw models set openai/gpt-5.5
openclaw models fallbacks clear
openclaw models set-image google/gemini-3.1-flash-image-preview
openclaw models status
```

## 7. Configure Telegram

Store the token in a local secret file. Do not commit the token.

```powershell
openclaw channels add --channel telegram --token-file C:\openclaw-secrets\telegram-bot-token.txt
openclaw channels status
```

## 8. Recreate Agents

Use `openclaw/agents.example.json` as the safe layout reference.

Required worker IDs:

- `orchestrator-agent`
- `research-agent`
- `doc-agent`
- `build-agent`
- `build-agent-2`
- `build-agent-3`
- `build-agent-4`
- `qa-agent`
- `browser-agent`
- `integrator-agent`
- `render-agent`
- `image-draft-agent`
- `image-final-agent`

## 9. Configure Obsidian

Create or sync the primary vault:

```text
C:\works
```

Create or sync the design vault:

```text
C:\design
```

Recommended GitHub remotes:

```text
works          -> C:\works
design         -> C:\design
openclaw-setup -> OpenClaw/OpenDesign/agent setup blueprint
```

On a new PC, clone the two vault repos directly into those paths:

```powershell
git clone <private-works-repo-url> C:\works
git clone <private-design-repo-url> C:\design
```

Then install Obsidian and open `C:\works` as the default vault. Open `C:\design` as the design reference vault when needed.

Current local baselines on this PC:

- `C:\works`: `bc217ba`
- `C:\design`: `02bbf03`

Do not sync:

- `C:\works\tmp`
- `C:\works\Logs`
- `C:\works\diag`
- `.obsidian\workspace.json`
- token, credential, auth, SQLite, DB, queue, lock, cache, and browser profile files

## 10. Validate

```powershell
openclaw config validate
openclaw health
openclaw gateway probe
openclaw channels status
openclaw agents list
openclaw models status
openclaw infer model run --local --model google/gemini-3-flash-preview --prompt "Reply with exactly: GEMINI_OK"
```

Expected:

- config valid
- gateway healthy
- Telegram connected
- 14 agents listed
- default model `openai/gpt-5.5`
- text fallbacks empty
- image model `google/gemini-3.1-flash-image-preview`
- Gemini test returns `GEMINI_OK`

## 11. Optional: OpenDesign

OpenDesign is optional for the OpenClaw/Obsidian baseline. Add it when visual design generation or browser-viewable design artifacts are needed.

Expected local daemon:

```text
http://127.0.0.1:7456
```

If using source/dev setup:

```powershell
pnpm install
pnpm tools-dev
Invoke-WebRequest -UseBasicParsing -Uri 'http://127.0.0.1:7456/' -TimeoutSec 5
```

After the daemon is running, verify OpenDesign projects, active context, agents, skills, and plugins from Codex/OpenDesign tools.
