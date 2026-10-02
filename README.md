# Taskboard: a dockerized full-stack app

A small task manager (create, complete, delete) split into three containers.

| Layer    | Technology         | Container  |
|----------|--------------------|------------|
| Frontend | HTML/CSS/JS + nginx | `frontend` |
| Backend  | Node.js + Express  | `backend`  |
| Database | PostgreSQL 16      | `db`       |

nginx serves the page and forwards every `/api/*` request to the backend,
which reads and writes PostgreSQL. Data is kept in a Docker volume (`pgdata`),
so it survives restarts.

## Run it

Requires Docker Desktop (or Docker Engine + Compose).

```bash
docker compose up --build
```

Open http://localhost:8080

## Useful commands

```bash
docker compose up --build -d     # run in the background
docker compose ps                # show running containers
docker compose logs -f backend   # follow backend logs
docker compose down              # stop everything
docker compose down -v           # stop and delete the database data
```

## API

| Method | Path             | Description            |
|--------|------------------|------------------------|
| GET    | /api/health      | Backend + DB check     |
| GET    | /api/tasks       | List tasks             |
| POST   | /api/tasks       | Create (`{"title":""}`)|
| PATCH  | /api/tasks/:id   | Toggle done            |
| DELETE | /api/tasks/:id   | Delete                 |

## Project layout

```
taskboard/
├── docker-compose.yml
├── db/init.sql
├── backend/   (Dockerfile, package.json, server.js)
└── frontend/  (Dockerfile, nginx.conf, index.html, style.css, app.js)
```
