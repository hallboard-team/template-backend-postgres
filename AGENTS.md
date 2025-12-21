# Agent Notes

## Project
- Template backend with Postgres.
- Devcontainer compose: `.devcontainer/docker/docker-compose.backend-postgres.yml`.

## Environment
- API service listens on `http://0.0.0.0:5000`.
- Postgres runs on `db:5432` with env-configured credentials.

## Expectations
- Prefer edits within the workspace; avoid touching generated files unless asked.
- Keep changes minimal and aligned with the existing devcontainer workflow.
