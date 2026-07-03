# stackmap
A full-stack engineering project designed to help identify a stack to build to enable you to target the roles you want. 

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

## stack choice for this build (meta I know)

StackMap uses React and TypeScript for a typed, interactive frontend; FastAPI and Pydantic for a structured backend and validation layer; PostgreSQL for relational job-advert analysis; and Docker/AWS for repeatable deployment and production-style infrastructure.

Note: The initial deployment will likely use a managed service for cost concerns, but will be built with containerization in mind moving forward to assist scalabiity. 

The stack was chosen because the product requires:

- a responsive interface for reviewing and correcting extracted data
- a reliable API layer for job advert submission and analysis
- strict validation of AI-generated structured output
- relational querying across many saved adverts
- room to add search, scoring, dashboards, and candidate profiles
- a deployment path that reflects real engineering environments
