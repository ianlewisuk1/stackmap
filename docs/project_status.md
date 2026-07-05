# StackMap — Project Status

A snapshot of where the project stands: the milestones we're building toward, what's
been accomplished so far, and what's likely next. For the full vision see
[`PLAN.md`](PLAN.md), for the MVP spec [`project_spec.md`](project_spec.md), for the
system design [`architecture.md`](architecture.md), and for the detailed history
[`change_log.md`](change_log.md).

**Last updated:** 2026-07-05
**Current phase:** Pre-MVP — scaffolding and documentation complete, feature work
not yet started.

## Milestones

### MVP
- A user can register and log in.
- A logged-in user can paste raw job description text and submit it.
- Submitted text is scanned against a curated technology list using keyword matching.
- The user can see which technologies were detected in their submission.

### V1
- Detected information is classified by role, not just by technology.
- Technology frequency is tracked across a user's submissions and correlated with roles.
- A "strength of recommendation" signal is surfaced per technology/role.
- Learning priorities are recommended from the aggregated data.

### Stretch
- Project recommendations paired with a recommended stack.
- Take in a project idea and recommend a stack against market data.
- Job-advert examples with stack-build recommendations.

## Accomplished so far

- **Repository & docs:** README, [`PLAN.md`](PLAN.md) (vision, milestones),
  [`project_spec.md`](project_spec.md) (MVP PRD/EDD — data model + API surface),
  [`architecture.md`](architecture.md) (system design), [`Claude.md`](../Claude.md)
  (working rules + architecture overview), and [`change_log.md`](change_log.md).
- **MVP scope resolved:** keyword/dictionary extraction (not LLM), a minimal data
  model, and user accounts from day one — see [`PLAN.md`](PLAN.md) → MVP Scope Decisions.
- **Backend scaffolding:** fresh Django `config` project (settings, URLs, WSGI/ASGI),
  `manage.py`, and `requirements.txt` (Django 6.0.6, DRF, django-cors-headers).
- **Tooling:** `.gitignore`, `.env.example`, and a local virtualenv.

## Current state

Boilerplate only. The backend runs on SQLite; `djangorestframework` and
`django-cors-headers` are installed via `requirements.txt` but **not yet wired into
`INSTALLED_APPS`**. There are no feature apps, models, API endpoints, seed data, or
Angular frontend yet.

## Likely next (toward MVP)

Ordered as small, single-ticket steps (per [`Claude.md`](../Claude.md) → Working Rules):

1. **Settings wiring** — add `rest_framework`, `corsheaders`, and DRF token auth to
   `INSTALLED_APPS`/middleware; configure default auth/permissions.
2. **Auth app** — `register` and `login` endpoints issuing DRF auth tokens.
3. **Job models** — `Technology`, `JobDescription`, `TechnologyMention` with migrations.
4. **Seed data** — data migration seeding the curated technology list (names + aliases).
5. **Extraction service** — case-insensitive, word-boundary-aware keyword matching
   against the curated list, with tests.
6. **Submission API** — `POST /api/jobs/` plus user-scoped `GET /api/jobs/` and
   `GET /api/jobs/<id>/`.

### After MVP
- Angular/TypeScript frontend against the API.
- Migrate from SQLite to PostgreSQL and add Docker Compose for local dev.
- Begin V1 work (role classification, frequency/correlation, recommendation strength).

_Keep this file in sync as tickets land — update "Accomplished so far", "Current
state", and "Likely next" alongside the relevant [`change_log.md`](change_log.md) entry._
