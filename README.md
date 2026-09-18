<<<<<<< HEAD
# JobApplicationAppE2E
FastAPI backend for tracking job applications, workflow automation, and application insights
=======
# Job Aggregation Backend

A production-structured FastAPI backend using PostgreSQL, SQLAlchemy 2 async ORM, asyncpg, Alembic, and Pydantic v2. Job-source connectors are intentionally not implemented; future connectors belong under `app/connectors`.

## Start the backend

1. Copy `.env.example` to `.env` when running outside Compose.
2. Start the API and PostgreSQL, including migrations:

```bash
docker compose up
```

The API is available at `http://localhost:8000`; interactive docs are at `/docs`, and the health check is at `/health`.

## Local development

Use Python 3.13 or newer:

```bash
python -m venv .venv
.venv\\Scripts\\activate
pip install -e ".[test]"
uvicorn app.main:app --reload
```

Set `DATABASE_URL` to a reachable PostgreSQL instance before starting locally. Apply migrations with `alembic upgrade head`.

## Tests

```bash
pytest
```

The test suite is structured for isolated API and database tests. The included health test does not require PostgreSQL; database-backed tests can use the Compose database or a dedicated test database.
>>>>>>> aedad3c (Initial V1 project setup)
