# OWASP FinBot CTF

See Collaborator Hub for details on this project: https://github.com/OWASP-ASI/FinBot-CTF-workstream


## Quick Start (Docker)

The fastest way to get running. Requires only Docker.

```bash
# 1. Configure environment
cp .env.example .env
# Edit .env — add your OPENAI_API_KEY at minimum

# 2a. SQLite (default, zero-config):
docker compose up

# 2b. PostgreSQL:
#     Set DATABASE_TYPE=postgresql in .env, then:
docker compose --profile postgres up
```

Platform runs at http://localhost:8000

### Playwright support (optional)

To enable OG image rendering (Playwright + Chromium), build the full image:

```bash
DOCKER_TARGET=app-full docker compose up --build
```

## Local Dev (without Docker)

### Prerequisites

Check if you have the required tools:
```bash
python scripts/check_prerequisites.py
```

### Setup

```bash
# Install dependencies
uv sync

# Setup database (defaults to sqlite, runs migrations)
uv run python scripts/db.py setup

# For PostgreSQL: start the database server first
docker compose up -d postgres
DATABASE_TYPE=postgresql uv run python scripts/db.py setup

# Start the platform
uv run python run.py
```

Platform runs at http://localhost:8000
