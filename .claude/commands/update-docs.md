---
description: Update the docs/ files after a milestone or major addition
argument-hint: [optional note on what changed]
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git log:*), Read, Edit, Write
---

Update the project documentation to reflect recent work, following the
"Keeping docs current" rule in `Claude.md`.

Context on what changed (may be empty — infer from git if so): $ARGUMENTS

Steps:

1. Determine what actually changed since the docs were last updated. Run
   `git status` and `git diff`, and check recent commits with
   `git log --oneline -15`. Focus on real code/config changes (new apps, models,
   API endpoints, dependencies, data-model/architecture/scope changes, or a met
   milestone) — not doc-only edits.
2. If nothing meaningful changed, say so and stop — do not invent updates.
3. Otherwise, update only the affected docs in `docs/`, per `Claude.md`:
   - `docs/change_log.md` — always add a dated entry (use today's date) under a
     heading, tagged Added / Changed / Fixed / Removed / Docs. Newest first.
   - `docs/project_status.md` — move completed items from "Likely next" to
     "Accomplished so far", refresh "Current state", the "Last updated" date, and
     the next-steps list.
   - `docs/architecture.md` — if components, tech stack, or data flow changed.
   - `docs/project_spec.md` — if the MVP data model or API surface changed.
   - `docs/PLAN.md` — if milestones, scope, or roadmap changed.
   - `README.md` — if local setup or run instructions changed.
4. Keep edits small, factual, and consistent with each doc's existing tone and
   format. Do not restructure docs or add speculative content.
5. Verify any markdown links you touch still resolve.
6. Summarize which files you changed and why. Do not commit or push — the user
   controls all pushes.
