# CLAUDE.md — UCA-WebPage

> Agent briefing. Read before touching code.
> Governance hub: `SAHearn1/rwfw-agent-governance`

## Repo Identity
- **Purpose:** United Community Academy (UCA) static web page
- **Tier:** 2 (active support)
- **Stack:** Static HTML + CSS + JavaScript
- **Related:** SAHearn1-UCA-WebPage (React version of this site)

## Critical Rules

- **Static site.** No build step, no framework.
- **School content.** Do not modify copy, branding, or contact info without human approval.
- **Test in browser** after every change.
- **No `git add .`**

## Dev Workflow
```bash
python -m http.server 8000
```

## Governance
Follow `AGENTS.md`.

## Operating Rules

**If you resolve a bug during this session, you MUST append an entry to `docs/INCIDENTS.md` before the session ends. This is non-negotiable. Session is not complete until the entry is committed.**

See Rule 7 in `AGENTS.md` (governance hub: `SAHearn1/rwfw-agent-governance`) for the full incident logging protocol.
