# Developer Guide

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start status -->
_Up to date._
<!-- sdlc:auto:end status -->

<!-- sdlc:auto:start source -->
Generated from commit `61a3c96` · model `claude-sonnet-5`
<!-- sdlc:auto:end source -->

<!-- sdlc:auto:start overview -->
simple calculator-1 is a Quorq-generated two-app repository: a Vite + React 19 SPA that implements an approved screen design running on seeded sample data, and a FastAPI backend scaffold that currently exposes only a health check endpoint (no approved backend architecture existed yet, so routers/models are stubs). The backend uses SQLAlchemy with a SQLite file by default (swappable to Postgres via DATABASE_URL), and the repo also ships a docker-compose.yml that can run a Postgres 16 container for that purpose.
<!-- sdlc:auto:end overview -->

<!-- sdlc:auto:start prerequisites -->
- Node.js (for Vite 6 / React 19 / npm scripts)
- Python 3.12
- pip
- Docker and Docker Compose (optional, only if using the Postgres service in docker-compose.yml)
<!-- sdlc:auto:end prerequisites -->

<!-- sdlc:auto:start setup -->
1. git clone <repo> && cd simple calculator-1
2. cd frontend && npm install
3. cd ../backend && pip install -r requirements.txt
4. (optional) copy .env.example to .env and adjust DATABASE_URL / ALLOWED_ORIGINS / VITE_API_BASE_URL / VITE_API_SECRET_KEY as needed
5. (optional) from repo root: docker-compose up -d db  # starts Postgres if you want to use it instead of the default SQLite file
<!-- sdlc:auto:end setup -->

<!-- sdlc:auto:start run -->
| Name | Command | Description |
|---|---|---|
| frontend dev | `cd frontend && npm run dev` | Starts the Vite dev server for the SPA |
| frontend build | `cd frontend && npm run build` | Bundles the app for production (does not typecheck) |
| frontend preview | `cd frontend && npm run preview` | Serves the production build locally |
| backend dev | `cd backend && uvicorn app.main:app --reload` | Runs the FastAPI service with auto-reload; creates SQLite tables on startup |
| db up | `docker-compose up -d db` | Starts a Postgres 16 container (app/app/app credentials) on port 5432 |
<!-- sdlc:auto:end run -->

<!-- sdlc:auto:start structure -->
| Path | Purpose |
|---|---|
| `backend` | FastAPI service: entrypoint, database setup, models, schemas, routers, and tests |
| `backend/app` | Application package: main.py (entrypoint + health route), database.py (engine/session), models.py, schemas.py |
| `backend/app/routers` | Generated routers, one per architecture component (currently empty) |
| `backend/tests` | Pytest test suite (currently just the health check) |
| `frontend` | Vite + React SPA for the approved UI design, running on seeded sample data |
| `frontend/src` | Application source: App.tsx, screens, lib helpers, styles |
| `frontend/src/lib` | Shared helpers: api.ts (API client), ui.tsx, icons.tsx, navigate.ts |
| `frontend/e2e` | Playwright end-to-end specs |
<!-- sdlc:auto:end structure -->

<!-- sdlc:auto:start conventions -->
- Backend follows one router per architecture component, one route per spec endpoint; unimplemented routes return a typed StubResponse rather than erroring, so the OpenAPI schema stays complete
- All SQLAlchemy models inherit from the shared Base in database.py; models.py is imported in main.py before Base.metadata.create_all so tables register
- Configuration is environment-variable driven: DATABASE_URL (backend DB), ALLOWED_ORIGINS (CORS), VITE_API_BASE_URL and VITE_API_SECRET_KEY (frontend API client)
- Backend defaults to a local SQLite file (app.db) so it runs with no external database; point DATABASE_URL at Postgres to change that
- Frontend component tests live beside the components they cover and are matched by Vitest's src/**/*.{test,spec}.{ts,tsx} pattern; Playwright specs live under e2e/ and are excluded from Vitest's run
- Frontend screens currently render seeded sample data; src/lib/api.ts is the prepared seam for wiring real backend calls
<!-- sdlc:auto:end conventions -->

<!-- sdlc:auto:start testing -->
| Name | Command | Description |
|---|---|---|
| frontend unit | `cd frontend && npm test` | Runs Vitest component tests |
| frontend lint | `cd frontend && npm run lint` | Runs ESLint over the frontend app (used as a dev gate) |
| frontend typecheck | `cd frontend && npm run typecheck` | Runs tsc --noEmit (not run by the build) |
| frontend e2e | `cd frontend && npm run test:e2e:install && npm run test:e2e` | Installs the Chromium browser then runs Playwright acceptance tests; boots backend and frontend locally unless E2E_BASE_URL is set |
| backend test | `cd backend && pytest` | Runs the backend pytest suite (includes coverage via pytest-cov per requirements.txt) |
| backend lint | `cd backend && ruff check .` | Lints the backend Python code |
| backend format | `cd backend && ruff format .` | Formats the backend Python code |
<!-- sdlc:auto:end testing -->

<!-- sdlc:auto:start troubleshooting -->
| Problem | Solution |
|---|---|
| CORS errors calling the backend from the frontend in development | By default the backend allows http://localhost:5173 and http://127.0.0.1:5173; if running the frontend on a different origin, set ALLOWED_ORIGINS on the backend to that comma-separated list |
| pytest fails with 'ModuleNotFoundError: app' when run from elsewhere | Run pytest from the backend/ directory; backend/pytest.ini sets pythonpath = . so `app` is importable only from there |
| npm run build succeeds but code has type errors | vite build does not typecheck; run `npm run typecheck` (tsc --noEmit) separately to catch issues like untyped useState |
| Playwright e2e tests fail to launch a browser | Run `npm run test:e2e:install` first to fetch Chromium before `npm run test:e2e` |
| Need Postgres instead of the default SQLite file | Run `docker-compose up -d db` and set DATABASE_URL (e.g. postgresql+psycopg://app:app@localhost:5432/app) before starting the backend |
<!-- sdlc:auto:end troubleshooting -->
