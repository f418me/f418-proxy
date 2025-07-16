# AlbyHub Docker Setup

This repository contains a minimal Docker Compose configuration for running [Alby Hub](https://github.com/getAlby/hub) behind a Caddy reverse proxy.

## Prerequisites

- Docker and Docker Compose installed on your host machine
- A domain name you control for HTTPS

## Setup

1. Clone this repository.
2. Copy `.env-example` to `.env` and adjust the values as needed. The most important settings are:
   - `BASE_URL` / `FRONTEND_URL` – the public URL of your Alby Hub instance.
   - `PORT` – the internal port used by the application (default: `8080`).
   - `JWT_SECRET` – a random secret used for authentication.
   - `CADDY_ACME_EMAIL` – email address for Let's Encrypt certificates.
3. Start the services with `docker compose up -d`.
4. Caddy will automatically obtain HTTPS certificates and forward traffic to the Alby Hub container.

Application data is stored in the `albyhub-data` directory. Caddy stores its configuration and certificates in `caddy/data` and `caddy/config`.
## Managing Services

Start the containers in the background with:

```bash
docker compose up -d
```

Stop and remove them:

```bash
docker compose down
```

To stop without removing containers, use:

```bash
docker compose stop
```

Monitor running containers:

```bash
docker compose ps
```

Follow logs in real time:

```bash
docker compose logs -f
```


## File Overview

- `docker-compose.yml` – defines the Alby Hub and Caddy services.
- `caddy/Caddyfile` – Caddy configuration for the reverse proxy.
- `.env-example` – environment variables example file.

