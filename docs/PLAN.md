# stackmap
A full-stack engineering project designed to help identify a stack to build to enable you to target the roles you want. 

Architecture and tech-stack detail live in [`architecture.md`](architecture.md).

## planned features

- User login and data retention
- Frontend will take in raw text from job adverts
- Extract relevent information
- Classify the information and roles
- Track technology frequency as well as correlation with roles
- Identify strength of recs
- Recomend learning priorities

## stretch goals

- Project recommendation to pair with recommended stack
- Take in a project idea and recommend stack in relation to available market data
- Job advertisement examples and stack build recs

## MVP Scope Decisions

Before starting implementation, the following scope questions were resolved:

- **Extraction approach:** Keyword/dictionary matching against a curated technology list, not LLM-based extraction. Deterministic and free of API cost/latency. The LLM-assisted extraction layer above remains a future upgrade, not part of the MVP.
- **Data model:** Start minimal — a job description, a curated technology list, and which technologies were matched in each job description. Company, Role, Category, and stack-count tables are deferred until this core pipeline is proven out.
- **Auth:** User accounts are built in from day one (not deferred), since job descriptions and their extraction results need to be tied to a user to support the "data retention" feature above.

No implementation plan has been written yet — these decisions narrow the MVP scope for when that planning happens.

## Success Milestones

### MVP

- A user can register and log in.
- A logged-in user can paste raw job description text and submit it.
- Submitted text is scanned against a curated technology list using keyword matching.
- The user can see which technologies were detected in their submitted job description.

### V1

- Detected information is classified by role, not just by technology.
- The app tracks technology frequency across a user's submissions and correlates technologies with roles.
- The app surfaces a "strength of recommendation" signal per technology/role rather than a flat match list.
- The app recommends learning priorities based on the aggregated frequency/correlation/strength data above.
