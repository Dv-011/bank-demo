# bank-demo

Dockerized multi-service demo app for DevOps practice:
- **web**: Nginx (static page)
- **backend**: FastAPI (`/health`)
- **db**: PostgreSQL (data persisted via volume)
- Uses **Docker Compose**, **networks**, **volumes**, **env-based config**
- Web container is configured to run as **non-root** (security best practice)

## Requirements
- Docker Engine
- Docker Compose v2 (`docker compose`)

Check:

docker --version
docker compose version
Project structure
markdown

bank-demo/
├── docker-compose.yml

├── .env.example
├── .gitignore
├── web/
│   ├── Dockerfile
│   ├── .dockerignore
│   └── index.html
└── backend/
    ├── Dockerfile
    ├── requirements.txt
    └── app.py
Configuration (.env)
Create local .env from example:


cp .env.example .env
Edit values if needed:

env

POSTGRES_DB=bankdb
POSTGRES_PASSWORD=changeme
.env is intentionally ignored by git to prevent leaking secrets.

Run
Build and start:


docker compose up -d --build
Status:



docker compose ps
Logs:



docker compose logs -f --tail=100
Stop (keep DB data):


docker compose down
Stop and remove DB data:


docker compose down -v
Endpoints
Web (Nginx): http://localhost:8080

Backend health: http://localhost:8000/health
(If backend port is not published in your compose file, test it from inside the network, see below.)

Test backend from inside Docker network (no host port required)


docker compose exec backend curl -s http://localhost:8000/health
Security notes
Web container runs as non-root.

No secrets are committed: .env is excluded by .gitignore.

DB data is persisted using a named volume.

Troubleshooting
Web container exits with permission errors
If you see Permission denied in nginx logs, it usually means nginx cannot write to cache/run directories when running as non-root. Ensure the Dockerfile creates required dirs and sets ownership.

Check logs:


docker compose logs web --tail=200
Ports not accessible from host
Verify that ports are published in docker-compose.yml:

web: 8080:80

backend (optional): 8000:8000

Then restart:


docker compose up -d --build
