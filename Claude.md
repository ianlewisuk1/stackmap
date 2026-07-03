// universal file for all information relative to the project that Claude might need to know. 

# CLAUDE.md

## Project

StackMap is a job-description analysis app. Users paste job descriptions, the app extracts technologies, stores the results, and shows stack trends.

## Stack

- Backend: Python, Django, Django REST Framework
- Frontend: TypeScript, Angular
- Database: PostgreSQL
- Local development: Docker Compose

## Working Rules

- Work in small, focused changes.
- Do not implement multiple major features at once.
- Explain the plan before changing code.
- Prefer simple, maintainable code.
- Add tests for meaningful backend logic.
- Update documentation when setup or architecture changes.

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