// universal file for all information relative to the project that Claude might need to know. 

# CLAUDE.md

## Project

StackMap is a job-description analysis app. Users paste job descriptions, the app extracts technologies, stores the results, and shows stack trends.

## Documentation

Project docs live in [`docs/`](docs/):

- [`docs/PLAN.md`](docs/PLAN.md) — over-arching product plan, roadmap, and milestones.
- [`docs/project_spec.md`](docs/project_spec.md) — MVP PRD/EDD (data model + API surface).
- [`docs/architecture.md`](docs/architecture.md) — canonical system architecture and tech stack.
- [`docs/project_status.md`](docs/project_status.md) — current progress and likely next steps.
- [`docs/change_log.md`](docs/change_log.md) — running record of development over time.

Setup/run instructions are in the root [`README.md`](README.md).

### Keeping docs current

After every **major milestone** (e.g. an MVP milestone met) or **major addition**
(a new app, model, API endpoint, dependency, or a data-model/architecture/scope
change), update the affected docs as part of the same change — don't let them drift:

- **`docs/change_log.md`** — always add a dated entry describing the change.
- **`docs/project_status.md`** — move the item from "Likely next" to "Accomplished
  so far", refresh "Current state", the "Last updated" date, and next steps.
- **`docs/architecture.md`** — when components, the tech stack, or data flow change.
- **`docs/project_spec.md`** — when the MVP data model or API surface changes.
- **`docs/PLAN.md`** — when milestones, scope, or the roadmap change.
- **`README.md`** — when local setup or run instructions change.

Prefer small doc updates landing alongside the code change over large catch-up edits.

## Stack

- Backend: Python, Django, Django REST Framework
- Frontend: TypeScript, Angular
- Database: PostgreSQL
- Local development: Docker Compose

## Architecture Overview

StackMap is a two-tier web app: an Angular/TypeScript single-page frontend talks
to a Django REST Framework JSON API, which persists to a relational database.
[`docs/architecture.md`](docs/architecture.md) is the canonical architecture doc;
[`docs/PLAN.md`](docs/PLAN.md) holds the long-term vision and
[`docs/project_spec.md`](docs/project_spec.md) the MVP PRD/EDD. This section summarizes them.

### Request flow

1. The Angular frontend collects raw job description text and calls the DRF API
   over HTTP, authenticating with a token obtained at login.
2. DRF views validate the request, enforce that users only touch their own data,
   and delegate to serializers/services.
3. A keyword-extraction service scans submitted text against a curated technology
   list (canonical names + aliases), using case-insensitive, word-boundary-aware
   matching. Extraction is deterministic — no LLM in the MVP.
4. The submission and its matched technologies are stored, scoped to the user, and
   returned in the response.

### Backend layout (`backend/`)

- `config/` — Django project: settings, root URL conf, WSGI/ASGI entrypoints.
- Feature apps (to be added one ticket at a time, e.g. an auth app and a jobs app)
  own their own models, serializers, views, and URLs, included into `config.urls`.

### Planned data model

- `Technology` — `name`, `slug`, `aliases`; curated and seeded via data migration,
  admin-editable.
- `JobDescription` — `user` (FK), `raw_text`, `created_at`.
- `TechnologyMention` — `job_description` (FK), `technology` (FK), `matched_text`,
  `created_at`; unique per (job_description, technology).

### Planned API surface

- `POST /api/auth/register/`, `POST /api/auth/login/` (DRF `TokenAuthentication`).
- `POST /api/jobs/` — submit text, returns the submission with matched technologies.
- `GET /api/jobs/` and `GET /api/jobs/<id>/` — the current user's own submissions.

### Environments

- Local dev: Docker Compose runs frontend, backend, and PostgreSQL together
  (introduced once the frontend exists).
- Production: managed SaaS hosting for frontend, backend, and PostgreSQL.

### Current state

Early scaffolding. The backend is a fresh Django project (`config`) on SQLite;
`djangorestframework` and `django-cors-headers` are in `requirements.txt` but not
yet wired into `INSTALLED_APPS`. No feature apps, models, API endpoints, or Angular
frontend exist yet — the sections above describe the target, not what is built.
Keep this overview in sync as tickets land (per Working Rules).

## Working Rules

- Work in small, focused changes.
- Do not implement multiple major features at once.
- Explain the plan before changing code.
- Prefer simple, maintainable code.
- Add tests for meaningful backend logic.
- Update documentation after major milestones or additions — see Documentation → "Keeping docs current".
- Do not push to GitHub, user to control all pushes. 

## AI Workflow

Claude should behave like a developer working from a ticket.

For each task:
1. Restate the goal.
2. Give a short implementation plan.
3. Make the smallest reasonable change.
4. Avoid unrelated refactors.
5. Explain changed files.
6. Tell me what command to run to test the change.

Do not move on to another task unless asked.
