# Api Service Must-Have Checklist

Base was copied from: [Dimildizio](https://github.com/Dimildizio/DS_course/blob/main/Templates/service_checkist.md)

## General

- [ ] Domain-Driven Design
- [ ] Use Pyproject.toml (separation of development vs. production dependencies)
- [ ] Docker + docker-compose setup
- [ ] ENV configuration via `.env` + Pydantic `BaseSettings`
- [ ] `.sh` script for quick local run (e.g., `run_local.sh`) of a simple example
- [ ] Makefile to run app, run pre-commit etc
- [ ] Minimal `README.md` with run instructions, curl example, input/output
- [ ] `.gitignore` includes `logs/`, `models/`, `.env`, `__pycache__/`, etc.

---

## API layer

- [ ] Async Litestar application
- [ ] Service readiness check endpoint (`/ready`)
- [ ] Service health check endpoint (`/health`)
- [ ] CRUD endpoints

## Database layer

- [ ] migrations with alembic
- [ ] Postgres database in docker container
- [ ] SQLALchemy with asyncpg and async_scoped_session

## Domain layer

- [ ] - pydantic models
- [ ] - business validations logic

---

## Code style

- [ ] use WPS linter (wemake-python-styleguide)
- [ ] use python 3.12 - 3.13 annotations (dont use Optional, use type_name | None instead Optional)
- [ ] write annotations and make sure code will pass such mypy checks
  - ignore_missing_imports = true
  - strict = true
  - local_partial_types = true
  - warn_unreachable = true
  - enable_error_code = [
"truthy-bool",
"truthy-iterable",
"redundant-expr",
"unused-awaitable",
"ignore-without-code",
"possibly-undefined",
"redundant-self",
"explicit-override",
"mutable-override",
"unimported-reveal",
"deprecated",
]

---

## Project Structure

This is example structure, you may add any files or folders, but follow Domain-Driven Design

```plaintext
project/
├── src/
│   ├── domain/                 # Domain layer
│   ├── infrastructure/         # Infrastructure layer
|   |   ├── web/                # Litestar logic
|   |   |   ├── api/            # Litestar routes
|   |   |   ├── config.py       # Litestar config
|   |   |   └── app.py          # Litestar app
|   |   ├── repositories/       # Postgres layer
|   |   |   ├── alembic/        # Alembic setup
|   |   |   ├── schemas/        # Schemas for each model
|   |   |   ├── repositories/   # CRUD for each model
|   |   |   └── db.py           # Db setup with sqlalchemy and asyncpg
│   └── config.py               # Global config
├── tests/                      # Pytest and integration tests
├── Makefile                    # Quick launch script
├── Dockerfile
├── docker-compose.yml
├── pyproject.toml              # Dependencies
├── .env
├── .dockerignore
└── README.md

```

## Testing

- [ ] use Pytest and branch-coverage
- [ ] use Polyfactory and Faker to generate data for models
- [ ] Load testing with Locust or K6
- [ ] Performance benchmarking guidelines or reports included

## Security & Stability

- [ ] Proper CORS policy  
- [ ] Rate limiting (e.g., slowapi) — optional  
- [ ] HTTPS-ready config for production use  
- [ ] Logging only enabled in debug/dev mode
- [ ] Docker runs only on `127.0.0.1` (not `0.0.0.0`) for local safety

## DevOps & Automation

- [ ] pre-commit hooks (ruff with format, isort, flake8)
