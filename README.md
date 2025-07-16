# AlbyHub Container Setup (Podman)

This repository contains a minimal Compose configuration for running [Alby Hub](https://github.com/getAlby/hub) and the f418 website behind a Caddy reverse proxy. It works with Podman Compose as a drop-in replacement for Docker Compose.

## Prerequisites

- Podman installed on your host machine (with the `podman compose` plugin)
- A domain name you control for HTTPS

## Setup

1. Clone this repository.
2. Copy `.env-example` to `.env` and adjust the values as needed. The most important settings are:
   - `BASE_URL` / `FRONTEND_URL` – the public URL of your Alby Hub instance.
   - `PORT` – the internal port used by the application (default: `8080`).
   - `JWT_SECRET` – a random secret used for authentication.
   - `CADDY_ACME_EMAIL` – email address for Let's Encrypt certificates.
3. Start the services with `podman compose up -d`.
4. Caddy will automatically obtain HTTPS certificates and forward traffic to the Alby Hub container.
5. The `f418-website` container is exposed via `https://f418.me` through the Caddy proxy.

Application data is stored in the `../albyhub` directory (relative to this repository). Caddy stores its configuration and certificates in `caddy/data` and `caddy/config`.
## Managing Services

Start the containers in the background with:

```bash
podman compose up -d
```

Stop and remove them:

```bash
podman compose down
```

To stop without removing containers, use:

```bash
podman compose stop
```

Monitor running containers:

```bash
podman compose ps
```

Follow logs in real time:

```bash
podman compose logs -f
```


## File Overview

- `docker-compose.yml` – Compose file compatible with Podman Compose (and Docker Compose) defining the Alby Hub, website and Caddy services.
- `caddy/Caddyfile` – Caddy configuration for the reverse proxy to `albyhub.f418.me` and `f418.me`.
- `.env-example` – environment variables example file.

