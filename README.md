# Dekunstmakers Network Infrastructure

Consolidated Docker Compose setup for the Dekunstmakers platform.

## Services

- **Traefik**: Reverse proxy with SSL termination
- **Postgres**: Database for Strapi
- **Strapi**: CMS backend (admin.dekunstmakers.com)
- **Frontend**: Nuxt static site (new.dekunstmakers.com)

## Setup

1. Copy `.env.example` to `.env` and fill in your values
2. Start all services: `docker-compose up -d`
3. Check logs: `docker-compose logs -f`

## Deployment

### Initial Setup on Server

1. Clone this repository to `/root/dekunstmakers-network` on your Hetzner server
2. Copy `.env.example` to `.env` and configure your environment variables
3. Run `docker-compose up -d` to start all services

### Automated Deployment

This repository includes a GitHub Actions workflow that automatically deploys infrastructure changes:

- **Automatic**: Triggers on pushes to `main` branch
- **Manual**: Can be triggered manually via GitHub Actions UI

The workflow will:
1. Copy `docker-compose.yml` to the server
2. Pull latest images for all services
3. Apply changes with `docker-compose up -d`

**Required GitHub Secrets:**
- `HETZNER_HOST`: Your Hetzner server IP/domain
- `HETZNER_USER`: SSH username (usually `root`)
- `HETZNER_SSH_KEY`: Private SSH key for server access

## Deploying Individual Services

### Deploy Frontend
```bash
docker-compose pull frontend
docker-compose up -d frontend
```

### Deploy Strapi
```bash
docker-compose pull strapi
docker-compose up -d strapi
```

## Network

All services are on the `dekunstmakers-network` bridge network, allowing them to communicate via service names.
