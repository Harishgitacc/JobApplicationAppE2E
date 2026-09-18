# Repository Guidelines

## Project State

- This is an incomplete FastAPI backend skeleton. Treat the README as the intended design, not proof that a referenced feature exists.
- Before claiming a workflow works, check that its entrypoints and supporting files exist. The documented API, migrations, and tests are not currently present in this checkout.
- Use Python 3.13 or newer.

## Architecture

- `app/api`: FastAPI routes, HTTP schemas, and request dependencies.
- `app/core`: settings and shared application infrastructure.
- `app/db`: asynchronous SQLAlchemy engine, sessions, models, and database dependencies.
- `app/connectors`: integrations with external job sources; keep source-specific logic here.
- `alembic/`: database migrations when migrations are added.
- `tests/`: pytest tests, separated into API and database-focused coverage.

Keep dependencies flowing toward core and infrastructure boundaries; do not put connector or HTTP concerns into shared database code. Follow existing package boundaries before adding new top-level modules.

## Commands

```text
python -m venv .venv
.venv\Scripts\activate
pip install -e ".[test]"
uvicorn app.main:app --reload
pytest
alembic upgrade head
docker compose up
```

Run `pytest` after behavioral changes. Ruff is configured for a 100-character line limit and Python 3.13, but is not declared as a project dependency; use `ruff check .` only when Ruff is available in the environment. No type checker is configured.

## Conventions

- Preserve async boundaries: use FastAPI async handlers and SQLAlchemy 2 async APIs for I/O.
- Use Pydantic v2 models for external data and `pydantic-settings` for configuration.
- Keep `DATABASE_URL` environment-aware: Compose uses the database hostname `db`; local execution needs a reachable host such as `localhost`.
- Do not commit secrets or treat the fixed Compose credentials as production-safe.
- Add focused tests for new behavior under `tests/`; do not assume PostgreSQL is available for unit/API tests unless the test requires it.

See [README.md](README.md) for the intended stack and developer workflows. Check [pyproject.toml](pyproject.toml), [Dockerfile](Dockerfile), and [docker-compose.yml](docker-compose.yml) when changing packaging, containers, or services.