# Change Log

A running record of StackMap's development over time. Add a new dated entry at the
top for each meaningful change (feature, model/API change, tooling, or docs that
affect setup or architecture). Newest first.

Format: group entries under a date heading, and tag each line with one of
**Added**, **Changed**, **Fixed**, **Removed**, or **Docs**.

## 2026-07-05

- **Added:** `/update-docs` project slash command (`.claude/commands/update-docs.md`)
  to refresh the `docs/` files after milestones/additions; listed it in `Claude.md`
  under "Custom commands".
- **Docs:** Added a "Keeping docs current" rule to `Claude.md` — docs in `docs/`
  are updated after major milestones/additions as part of the same change.
- **Changed:** Moved all project docs into `docs/` (`PLAN.md`, `project_spec.md`,
  `architecture.md`, `change_log.md`, `project_status.md`); `Claude.md` and
  `README.md` stay in the root. Added a Documentation index to `Claude.md` linking
  every doc and fixed cross-references.
- **Docs:** Added `project_status.md` — milestones, what's accomplished, current
  state, and the likely next steps toward MVP.
- **Docs:** Added `architecture.md` as the canonical architecture doc and moved the
  tech-stack detail into it from `PLAN.md`, leaving `PLAN.md` as the over-arching
  plan. Updated cross-references in `CLAUDE.md` and `PLAN.md`.
- **Docs:** Added an Architecture Overview to `CLAUDE.md` (request flow, backend
  layout, planned data model, API surface, environments, and current state), with
  links to `PLAN.md` and `project_spec.md`.
- **Docs:** Added `project_spec.md` — MVP PRD/EDD (problem, goals, user flow, data
  model, API surface).
- **Docs:** Refined `PLAN.md` MVP scope decisions and added an `.env.example`.
- **Added:** Started this change log.

## 2026-07-03

- **Added:** Django boilerplate — `config` project (settings, URLs, WSGI/ASGI),
  `manage.py`, `.venv`, and `requirements.txt` (Django 6.0.6, DRF, cors-headers).
- **Added:** `PLAN.md` capturing the long-term vision, tech-stack rationale, and
  success milestones.
- **Docs:** README updated with product spec, tech stack, and step-by-step local
  launch instructions.
- **Changed:** Updated `.gitignore`.

## 2026-07-03 — Project start

- **Added:** Initial repository and first `CLAUDE.md` with project instructions and
  AI workflow.
