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

## Tech Stack

### Frontend: TypeScript + Angular

TypeScript provides type safety across the frontend, while Angular gives the application a structured framework with routing, forms, services, and API communication built in.

### Backend: Python + Django + Django REST Framework

Python is widely used for backend development, automation, and AI workflows. Django provides a mature backend structure, ORM, migrations, and admin tooling, while Django REST Framework exposes the backend through a clean API.

### Database: PostgreSQL

The application data is naturally relational. Job specs, companies, technologies, categories, and stack counts all connect to each other, making PostgreSQL a strong fit for structured querying and reliable storage.

### Local Development: Docker + Docker Compose

Docker allows the frontend, backend, and database to run together in a consistent local environment that closely resembles a real deployment setup.

### Live Deployment: Managed SaaS Platforms

The live site will use managed hosting for the frontend, backend, and database to avoid unnecessary infrastructure cost and complexity while the product is still early.

### Future AI Layer: LLM-assisted Extraction

An AI-assisted extraction layer can help identify, categorize, and normalize technology mentions from messy job descriptions, making the analysis faster and more consistent.