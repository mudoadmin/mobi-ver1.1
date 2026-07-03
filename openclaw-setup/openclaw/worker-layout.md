# OpenClaw Agent Worker Layout

Snapshot date: 2026-07-04 KST

## Defaults

- Default model: `openai/gpt-5.5`
- Text fallbacks: none
- Image model: `google/gemini-3.1-flash-image-preview`
- Subagent delegation: `prefer`
- Max concurrent subagents: `5`
- Gateway: `ws://127.0.0.1:18789`
- Dashboard: `http://127.0.0.1:18789/`

## Worker Map

| Agent ID | Model | Workspace | Role |
|---|---|---|---|
| `main` | `openai/gpt-5.5` | `%USERPROFILE%\.openclaw\workspace` | User conversation, routing, status, cancellation, final reporting |
| `orchestrator-agent` | `openai/gpt-5.5` | `%USERPROFILE%\.openclaw\workspace` | Criteria, worker assignment, queue state, progress tracking, result collection |
| `research-agent` | `openai/gpt-5.5` | `%USERPROFILE%\.openclaw\workspace-research-agent` | Research, source discovery, evidence collection, structured notes |
| `doc-agent` | `openai/gpt-5.5` | `%USERPROFILE%\.openclaw\workspace-doc-agent` | Documents, PPT outlines, reports, summaries, presentation copy |
| `build-agent` | `openai/gpt-5.5` | `%USERPROFILE%\.openclaw\workspace-build-agent` | File generation, scripts, transforms, artifact assembly, verification |
| `build-agent-2` | `openai/gpt-5.5` | `%USERPROFILE%\.openclaw\workspace-build-agent-2` | Parallel builder lane 2 |
| `build-agent-3` | `openai/gpt-5.5` | `%USERPROFILE%\.openclaw\workspace-build-agent-3` | Parallel builder lane 3 |
| `build-agent-4` | `openai/gpt-5.5` | `%USERPROFILE%\.openclaw\workspace-build-agent-4` | Parallel builder lane 4 |
| `qa-agent` | `openai/gpt-5.5` | `%USERPROFILE%\.openclaw\workspace-qa-agent` | Review, validation, risk checks, numbers, sources, file QA |
| `browser-agent` | `openai/gpt-5.5` | `%USERPROFILE%\.openclaw\workspace-browser-agent` | Browser, map capture, login-bound checks, external UI workflows, screenshots |
| `integrator-agent` | `openai/gpt-5.5` | `%USERPROFILE%\.openclaw\workspace-integrator-agent` | Final PPTX integration, partial-deck merge, style unification |
| `render-agent` | `openai/gpt-5.5` | `%USERPROFILE%\.openclaw\workspace-render-agent` | PPTX to PDF, PNG previews, contact sheets, packages, export verification |
| `image-draft-agent` | `google/gemini-3-flash-preview` | `%USERPROFILE%\.openclaw\workspace-image-draft-agent` | Visual direction, prompt packs, mood variants, fast image candidates |
| `image-final-agent` | `google/gemini-3.1-pro-preview` | `%USERPROFILE%\.openclaw\workspace-image-final-agent` | Final hero images, high-quality edits, premium visual polish |

## Routing Rules

Builders own implementation and artifact assembly. Builders do not own:

- design direction
- visual concept exploration
- prompt packs
- generated image production

Image agents own:

- visual directions
- prompt packs
- draft image candidates
- selected final bitmap assets

Integrator owns:

- final PPTX assembly
- slide/deck merge
- style normalization
- Korean layout consistency

Render owns:

- PPTX to PDF export
- PNG previews
- contact sheets
- package verification

QA owns:

- final quality gate
- factual checks
- source checks
- number checks
- layout and output-file checks

## Visual PPT Workflow

1. `doc-agent`: audience, storyline, slide purpose, tone, copy reduction.
2. `image-draft-agent`: visual concepts, prompt packs, draft assets when needed.
3. `image-final-agent`: selected final hero assets or premium polish only when needed.
4. `build-agent`: slide/file implementation using approved design and image inputs.
5. `integrator-agent`: final PPTX assembly and style unification.
6. `render-agent`: PDF/PNG/contact sheet export and package verification.
7. `qa-agent`: final quality gate.

