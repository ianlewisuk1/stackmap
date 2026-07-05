# StackMap — Project Spec

A lightweight PRD + EDD for the MVP. This is the single doc to hand Claude Code when starting a build session — it says *what* to build and *how it's shaped*, without the ceremony of separate product/design docs. See `PLAN.md` for the longer-term vision and `CLAUDE.md` for how Claude Code should behave while working from this spec.

## Problem

Job seekers don't have a clear, data-driven way to see which technologies actually show up across the roles they're targeting. StackMap lets a user paste raw job description text and get back the technologies mentioned in it, building toward stack/role trend analysis over time.

## Goals (MVP)

- A user can register, log in, and submit job description text.
- The app detects which known technologies are mentioned in that text.
- The user can see the detected technologies for each submission they've made.

## Non-goals (MVP)

- No role classification, frequency/correlation tracking, or learning-priority recommendations — these are V1 (see `PLAN.md` → Success Milestones).
- No LLM-based extraction — keyword/dictionary matching only.
- No Angular frontend, Docker Compose, or PostgreSQL migration yet — backend API against sqlite first.
- No admin-facing tooling beyond Django's built-in `/admin/`.

## User flow

1. User registers → logs in → receives an auth token.
2. User POSTs raw job description text to the API.
3. App scans the text against a curated technology list (name + known aliases).
4. App stores the submission and the matched technologies, scoped to that user.
5. User can list/retrieve their own submissions and see which technologies were detected in each.

## Functional requirements

- **Auth:** register, log in. Django's built-in `User` model — no custom user model needed for MVP.
- **Submit:** authenticated users can POST raw text; unauthenticated requests are rejected.
- **Extract:** matching is case-insensitive, word-boundary-aware (e.g. "Java" must not match inside "JavaScript"), and checks both canonical names and aliases (e.g. "JS" → JavaScript).
- **Retrieve:** a user can only see their own submissions, never another user's.

## Proposed data model

Minimal, per the MVP scope decision in `PLAN.md` — no Company/Role/Category/StackCount tables yet.

- `Technology`: `name`, `slug`, `aliases` (list) — curated, seeded via data migration so it runs automatically and stays admin-editable.
- `JobDescription`: `user` (FK), `raw_text`, `created_at`.
- `TechnologyMention`: `job_description` (FK), `technology` (FK), `matched_text`, `created_at` — join between a submission and the technologies found in it, unique per (job_description, technology).

## Proposed API surface

- `POST /api/auth/register/` — create a user.
- `POST /api/auth/login/` — obtain an auth token (DRF `TokenAuthentication`, not JWT — no dependency to add, no expiry/refresh requirement yet to justify the extra complexity).
- `POST /api/jobs/` — submit raw text; returns the created submission with matched technologies.
- `GET /api/jobs/` / `GET /api/jobs/<id>/` — list/retrieve the current user's own submissions.

## Tech stack

Python/Django/DRF backend, Angular/TypeScript frontend (not started), PostgreSQL in production (sqlite for now), Docker Compose for local dev once the frontend exists. Full rationale in `PLAN.md` → Tech Stack.

## Success criteria

Matches the MVP milestones in `PLAN.md`: a user can register, log in, submit text, and see which curated technologies were detected in it. V1 milestones (role classification, frequency/correlation, recommendation strength, learning-priority recs) are out of scope until MVP is working end to end.

## Building this with Claude Code

- Work one ticket at a time (e.g. "settings wiring", "auth app", "job models", "seed data", "extraction service", "submission API") — don't bundle multiple of these into one change. See `CLAUDE.md` → Working Rules.
- Each ticket should be restated as a goal + short plan before code changes, land with tests for any new backend logic, and end with the command to verify it (usually `python manage.py test`, sometimes a `curl` example against a running server).
- Update this spec (or `PLAN.md`) if a ticket changes the data model, API surface, or scope described above — don't let this doc drift out of sync with what's actually built.
