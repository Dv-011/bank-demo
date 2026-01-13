# bank-demo

Dockerized multi-service demo app for DevOps practice:

- **web**: Nginx (static page)
- **backend**: FastAPI (`/health`)
- **db**: PostgreSQL (data persisted via volume)
- Uses **Docker Compose**, **networks**, **volumes**, **env-based config**
- Web container is configured to run as **non-root** (security best practice)

---

## Requirements

- Docker Engine
- Docker Compose v2 (`docker compose`)

Check:

```bash
docker --version
docker compose version

Project structure

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

POSTGRES_DB=bankdb
POSTGRES_PASSWORD=changeme

.env is intentionally ignored by git to prevent leaking secrets.
