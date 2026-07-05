# StackMap — Architecture

This document records StackMap's current architecture: how the pieces fit together
and the technology chosen for each layer. For the over-arching product plan and
roadmap see [`PLAN.md`](PLAN.md); for the MVP data model and API surface see
[`project_spec.md`](project_spec.md).

## Shape

StackMap is a two-tier web application:

- An **Angular / TypeScript** single-page frontend collects raw job description
  text and renders the detected technologies.
- A **Django REST Framework** JSON API handles authentication, request validation,
  technology extraction, and persistence.
- A **PostgreSQL** database stores users, job descriptions, the curated technology
  list, and the technologies matched per submission.

The frontend talks to the backend over HTTP using token authentication. On
submission, the backend runs a deterministic keyword-extraction pass over the text
against the curated technology list (canonical names + aliases) and stores the
matches, scoped to the user. See [`project_spec.md`](project_spec.md) for the
request/response detail.

## Tech stack

### Frontend: TypeScript + Angular

TypeScript provides type safety across the frontend, while Angular gives the
application a structured framework with routing, forms, services, and API
communication built in.

### Backend: Python + Django + Django REST Framework

Python is widely used for backend development, automation, and AI workflows. Django
provides a mature backend structure, ORM, migrations, and admin tooling, while
Django REST Framework exposes the backend through a clean API.

### Database: PostgreSQL

The application data is naturally relational. Job specs, companies, technologies,
categories, and stack counts all connect to each other, making PostgreSQL a strong
fit for structured querying and reliable storage.

### Local development: Docker + Docker Compose

Docker allows the frontend, backend, and database to run together in a consistent
local environment that closely resembles a real deployment setup.

### Live deployment: Managed SaaS platforms

The live site will use managed hosting for the frontend, backend, and database to
avoid unnecessary infrastructure cost and complexity while the product is still
early.

### Future AI layer: LLM-assisted extraction

An AI-assisted extraction layer can help identify, categorize, and normalize
technology mentions from messy job descriptions, making the analysis faster and
more consistent. This is a future upgrade — the MVP uses deterministic keyword
matching only (see [`PLAN.md`](PLAN.md) → MVP Scope Decisions).

## Current state

Early scaffolding. The backend is a fresh Django `config` project on SQLite;
`djangorestframework` and `django-cors-headers` are in `requirements.txt` but not
yet wired into `INSTALLED_APPS`. No feature apps, models, API endpoints, or Angular
frontend exist yet — the stack above describes the target, not what is built. Keep
this document in sync as tickets land.
