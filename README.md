# Docker Internship Project — Task Manager

A complete internship-ready web application demonstrating Docker and containerization with:

- Frontend: HTML, CSS, JavaScript
- Backend: Node.js + Express
- Database: MySQL 8
- Containerization: Docker
- Orchestration: Docker Compose
- Persistent storage: Docker volume
- Networking: Docker Compose service network
- Configuration: Environment variables

## Project architecture

Browser → Frontend container → Backend container → MySQL container → MySQL volume

## Project structure

```text
docker-internship-project/
├── frontend/
│   ├── Dockerfile
│   ├── nginx.conf
│   ├── index.html
│   ├── style.css
│   └── app.js
├── backend/
│   ├── Dockerfile
│   ├── package.json
│   ├── server.js
│   └── .dockerignore
├── db/
│   └── init.sql
├── .env.example
├── .gitignore
├── .dockerignore
├── docker-compose.yml
└── README.md
```

## Prerequisites

Install Docker Desktop on Windows/macOS, or Docker Engine + Compose on Linux.

Verify:

```bash
docker --version
docker compose version
```

## Run the project

1. Copy `.env.example` to `.env`.

Windows CMD:

```cmd
copy .env.example .env
```

PowerShell:

```powershell
Copy-Item .env.example .env
```

Linux/macOS:

```bash
cp .env.example .env
```

2. Start all services:

```bash
docker compose up -d --build
```

3. Check containers:

```bash
docker compose ps
```

4. Open:

```text
http://localhost:3000
```

The frontend is served by Nginx. It proxies `/api` requests to the Node.js backend.

## Useful commands

View logs:

```bash
docker compose logs -f
```

Backend only:

```bash
docker compose logs -f backend
```

Database only:

```bash
docker compose logs -f db
```

Stop:

```bash
docker compose down
```

Stop and remove the database volume too:

```bash
docker compose down -v
```

Rebuild:

```bash
docker compose up -d --build
```

List images:

```bash
docker images
```

List containers:

```bash
docker ps
```

Enter the backend container:

```bash
docker compose exec backend sh
```

Open MySQL:

```bash
docker compose exec db mysql -uappuser -papp_password internship_db
```

## API endpoints

| Method | Endpoint | Purpose |
|---|---|---|
| GET | `/api/health` | Health check |
| GET | `/api/tasks` | Get all tasks |
| POST | `/api/tasks` | Create a task |
| PUT | `/api/tasks/:id` | Update a task |
| DELETE | `/api/tasks/:id` | Delete a task |

Example:

```bash
curl http://localhost:3000/api/health
```

Create a task:

```bash
curl -X POST http://localhost:3000/api/tasks ^
  -H "Content-Type: application/json" ^
  -d "{\"title\":\"Docker documentation\",\"description\":\"Complete internship documentation\",\"status\":\"pending\"}"
```

For Linux/macOS, use `\` instead of `^` for line continuation.

## Docker concepts demonstrated

### Image

An image is the packaged template used to create a container.

### Container

A container is a running instance of an image.

### Network

Compose creates a private network so `frontend`, `backend`, and `db` can communicate by service name.

### Volume

`mysql_data` stores database files outside the disposable container layer.

### Environment variables

Database credentials and service settings are provided through `.env` and Compose.

## Internship workflow

```text
Source Code
    ↓
Dockerfile
    ↓
Docker Image
    ↓
Docker Container
    ↓
Docker Compose
    ↓
Running Application
```

## Troubleshooting

If port 3000 is already in use, change the frontend port in `docker-compose.yml`:

```yaml
ports:
  - "8080:80"
```

Then open:

```text
http://localhost:8080
```

If the database has stale data and you want a clean database:

```bash
docker compose down -v
docker compose up -d --build
```

## Internship deliverables

- Source code
- Dockerfiles
- Docker Compose configuration
- MySQL database
- Persistent volume
- REST API
- Responsive frontend
- README/documentation
- Docker commands and testing evidence
