# ML Service Must-Have Checklist

Base was copied from: [Dimildizio](https://github.com/Dimildizio/DS_course/blob/main/Templates/service_checkist.md)

## General

- [ ] Async FastAPI application
- [ ] Use Pyproject.toml (separation of development vs. production dependencies)
- [ ] Minimum 4 workers (Gunicorn + Uvicorn worker)
- [ ] Docker + docker-compose setup
- [ ] ENV configuration via `.env` + Pydantic `BaseSettings`
- [ ] `.sh` script for quick local run (e.g., `run_local.sh`) of a simple example
- [ ] Makefile to run app, run pre-commit etc
- [ ] Minimal `README.md` with run instructions, curl example, input/output
- [ ] `.gitignore` includes `logs/`, `models/`, `.env`, `__pycache__/`, etc.
- [ ] Version endpoint (/version) for easy identification of running model/service

---

## Model Management

- [ ] Heavy files (model, index, etc.) loaded once on startup
- [ ] Model readiness check endpoint (`/ready`)
- [ ] Service health check endpoint (`/health`)
- [ ] Asynchronous model initialization supported
- [ ] Graceful shutdown of resources/models (GPU-bound resources)
- [ ] Endpoint for retrieving model metadata (e.g., model version, date trained, hyperparameters)

---

## Code style

- [ ] use WPS linter (wemake-python-styleguide)
- [ ] use python 3.12  3.13 annotations (dont use Optional, use type_name | None instead Optional)
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

This is example structure, you may add any files or folders

```plaintext
project/
├── src/
│   ├── api/              # FastAPI routes
│   ├── config/           # ENV and settings
│   ├── data/             # Input/output processing
|   |   ├── models/        # Model files (gitignored)
|   |   ├── datasets/        # Dataset files (gitignored)
│   ├── inference/        # Model and prediction logic
│   ├── utils/            # Utility and helper functions
|   ├── scripts/          # Utility scripts (e.g., model download, maintenance)
│   └── main.py           # FastAPI entrypoint
├── logs/                 # Logs and saved outputs (gitignored)
├── tests/                # Unit and integration tests
├── notebooks/            # Jupyter notebooks (optional)
├── run_local.sh          # Quick launch script
├── Dockerfile
├── docker-compose.yml
├── pyproject.toml      # Dependencies
├── .env
├── .dockerignore
└── README.md

```

## Data Handling

- [ ] Input validation via Pydantic  
- [ ] Error handling with readable JSON responses  
- [ ] Logging of input/output can be disabled via ENV flag  
- [ ] Output must be JSON-serializable  
- [ ] Multipart/form support for images/files
- [ ] Clearly defined response schemas (Pydantic response models)
- [ ] Optional input size limitations or validations (e.g., file-size limit, dimensions)

## Testing

- [ ] use Pytest and branch-coverage
- [ ] Input validation tests (e.g., empty, corrupted input)  
- [ ] Load testing with Locust or K6
- [ ] Performance benchmarking guidelines or reports included

## Security & Stability

- [ ] Proper CORS policy  
- [ ] Rate limiting (e.g., slowapi) — optional  
- [ ] HTTPS-ready config for production use  
- [ ] Ability to disable graphical/statistical tools via ENV  
- [ ] Logging only enabled in debug/dev mode
- [ ] Docker runs only on `127.0.0.1` (not `0.0.0.0`) for local safety

## DevOps & Automation

- [ ] pre-commit hooks (ruff with format, isort, flake8)
