# OpenDesign Setup

Snapshot date: 2026-07-04 KST

OpenDesign is a local-first design workspace. In this Codex integration, OpenDesign projects contain rendered artifacts such as HTML, JSX, CSS, SVG, Markdown, and referenced source files.

## Current Local Status

- OpenDesign daemon expected URL: `http://127.0.0.1:7456`
- Current status during this snapshot: daemon not reachable
- Tool hint from the integration: start it with `pnpm tools-dev`
- Node.js is installed on this PC.
- pnpm is installed on this PC.

## Install / Start Checklist

Use one of these paths depending on how OpenDesign is distributed on the target computer.

### Packaged App Path

1. Install or open the OpenDesign desktop/local app.
2. Confirm that the local daemon starts.
3. Verify that Codex can reach `http://127.0.0.1:7456`.
4. In Codex, use OpenDesign tools to check:
   - active context
   - project list
   - available agents
   - available skills/plugins

### Source / Dev Path

1. Install prerequisites:
   - Node.js
   - pnpm
   - Git
2. Clone or copy the OpenDesign source folder.
3. Install dependencies:

```powershell
pnpm install
```

4. Start the OpenDesign daemon:

```powershell
pnpm tools-dev
```

5. Verify daemon reachability:

```powershell
Invoke-WebRequest -UseBasicParsing -Uri 'http://127.0.0.1:7456/' -TimeoutSec 5
```

## Agent CLI Setup

OpenDesign can spawn its own agent runs. Do not guess available agents. After OpenDesign is running, ask it for installed and unavailable agents.

Expected checks:

- list available OpenDesign agents
- include unavailable agents to see install URLs
- install only the agent CLIs you actually plan to use

Recommended default:

- Keep Codex as the main quality lane.
- Use OpenDesign for design artifact generation/refinement.
- Use Gemini only for image/visual assets unless intentionally changed.

## Workflow Notes

OpenDesign natively produces browser-viewable design artifacts, not binary Office files.

Good OpenDesign outputs:

- HTML/SVG visual decks
- landing-page style design artifacts
- editable source bundles
- design prototypes
- visual concept variants

When the user asks for `PPT`, `deck`, `slides`, `PDF`, or `doc`, clarify whether they want:

- browser-viewable OpenDesign output, or
- a real `.pptx`, `.pdf`, or `.docx` binary exported by the Codex/OpenClaw artifact pipeline.

If a real PPTX/PDF is needed, use OpenDesign for design generation only, then hand off to:

1. `build-agent`
2. `integrator-agent`
3. `render-agent`
4. `qa-agent`

## Verification Checklist

After OpenDesign is started:

```text
OpenDesign daemon reachable at http://127.0.0.1:7456
OpenDesign project list works
OpenDesign active context works after opening a project
OpenDesign available agents list works
OpenDesign available skills/plugins list works
```

## Security Notes

Do not save these in OpenDesign projects:

- API keys
- OAuth tokens
- Telegram bot tokens
- passwords
- private credentials
- raw credential files

