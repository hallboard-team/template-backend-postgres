# .NET + PostgreSQL Dev Template

Docker-first development template for Hallboard .NET backends backed by PostgreSQL.  
Drop your solution inside `src/`, start the provided compose stack, and you get a ready-to-code environment that runs the API in the `ghcr.io/hallboard-team/dotnet:<version>-sdk` dev container alongside PostgreSQL.

## Repository Layout
- `src/` – place your .NET solution or clone an existing backend here (`src/Mvp` is a placeholder).
- `.devcontainer/` – Dev Container + Docker Compose definitions (`devcontainer.json`, `docker-compose.backend-postgres.yml`, helper script).
- `.devcontainer/docker/pull-start-backend-postgres-dev.sh` – pulls the pinned GHCR SDK image and starts the API + Postgres stack with sane defaults.

## Prerequisites
- Docker Desktop or Docker Engine with Compose v2.
- VS Code with the Dev Containers extension (optional, but recommended for attaching to the running container).
- Bash shell (for running the helper script on macOS/Linux or Git Bash on Windows).

## Quick Start
1. Put your backend solution under `src/` (or replace `src/Mvp` with your project).
2. From `.devcontainer/docker/`, run:
   ```bash
   ./pull-start-backend-postgres-dev.sh
   ```
   - Arguments let you override ports, .NET SDK version, DB credentials, and the project name:  
     `./pull-start-backend-postgres-dev.sh [api_port] [dotnet_version] [postgres_version] [db_host_port] [db_user] [db_password] [db_name] [project_name]`
   - Example: `./pull-start-backend-postgres-dev.sh 5001 10.0 17 5435 myuser mypass mydb myproject`
3. In VS Code run `code .` and re-open the folder in the Dev Container when prompted, or attach to the running container via the Dev Containers extension.
4. Inside the container, restore/build/test your solution as usual (`dotnet restore`, `dotnet test`, etc.).

To stop everything: `docker compose -p <project_name> -f .devcontainer/docker/docker-compose.backend-postgres.yml down`.

## Environment Defaults
- API container image: `ghcr.io/hallboard-team/dotnet:${DOTNET_VERSION:-10.0}-sdk`
- API port: `5000` (override with `API_PORT`)
- PostgreSQL: `postgres:${POSTGRES_VERSION:-17}-alpine`
- Host DB port: `5433` (override with `DB_HOST_PORT`)
- DB credentials: `backend_postgres_user/backend_postgres_password`
- DB name: `backend_postgres_db`
- Project name: `template_backend_postgres` (override with `COMPOSE_PROJECT_NAME`)
- Connection string exposed to the API container via `ConnectionStrings__Default`.

Set any of these values in `.devcontainer/docker/.env` or pass them as arguments to the helper script before launching the stack.

## Tips
- If Docker fails to pull the SDK image, authenticate with GHCR (`echo $PAT | docker login ghcr.io -u USERNAME --password-stdin`).
- The script ensures the repo ownership matches your UID to keep Dev Containers happy—follow the on-screen `chown` suggestion if needed.
- Share the VS Code extensions list in `.devcontainer/devcontainer.json` so teammates get the same editing experience automatically.
