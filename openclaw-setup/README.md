# OpenClaw Workstation Setup

Last updated: 2026-07-04 KST

This repo is the safe, shareable setup blueprint for Jongwoo's OpenClaw workstation.

It intentionally stores:

- OpenClaw agent and worker layout
- Safe copies of each agent's `AGENTS.md`
- Model routing policy
- PPT/image production workflow
- Obsidian vault convention
- Gateway hidden-startup notes
- OpenDesign install and verification notes
- Restore and validation checklist

It intentionally does not store:

- API keys
- OAuth access or refresh tokens
- Telegram bot tokens
- passwords
- private credentials
- raw `.openclaw/credentials`, `.openclaw/identity`, queue, lock, or log files
- raw `auth-profiles.json`

## Current Policy

- Heavy and quality-sensitive work stays on Codex/OpenAI: `openai/gpt-5.5`.
- Gemini is not a text fallback.
- Gemini is used for image and visual asset lanes only.
- Builders do not create images or own design direction.
- Image agents create visual directions, prompt packs, drafts, and selected final image assets.
- Integrator assembles the final PPTX.
- Render agent exports PDF/PNG/contact sheets and verifies output packages.
- QA agent owns the final quality gate.

## Files

- `openclaw/worker-layout.md`: human-readable agent and worker map.
- `openclaw/agents.example.json`: sanitized agent config template.
- `openclaw/agents.current.safe.json`: current safe agent layout captured from this PC.
- `openclaw/agent-instructions/<agent-id>/AGENTS.md`: safe agent instruction files copied from this PC.
- `openclaw/models.example.json`: sanitized model/provider template.
- `openclaw/startup-hidden-gateway.md`: hidden OpenClaw Gateway startup setup.
- `opendesign/README.md`: OpenDesign install, daemon, and workflow notes.
- `obsidian/README.md`: Obsidian vault convention.
- `restore-checklist.md`: new PC restore checklist.
- `.env.example`: secret names only, no secret values.

## Source of Truth

Use this repo as the versioned source of truth. Use Notion as the readable runbook.

## Companion Vault Repositories

The workstation uses three versioned local sources:

- `C:\works`: primary Obsidian vault, local baseline commit `bc217ba`.
- `C:\design`: design Obsidian vault, local baseline commit `02bbf03`.
- this repo: OpenClaw/OpenDesign/agent setup blueprint.

Recommended GitHub layout:

- private repo `works` for `C:\works`
- private repo `design` for `C:\design`
- private repo `openclaw-setup` for this setup blueprint

Do not push raw `%USERPROFILE%\.openclaw\agents` as a full folder. It contains runtime state, caches, sessions, SQLite files, and credential-adjacent data. Use `openclaw/agent-instructions` and `openclaw/agents.current.safe.json` instead.
