# Dekunstmakers Network Infrastructure

Consolidated Docker Compose setup for the Dekunstmakers platform.

## Services

- **Traefik**: Reverse proxy with SSL termination
- **Postgres**: Database for Strapi
- **Strapi**: CMS backend (admin.dekunstmakers.com)
- **Frontend**: Nuxt static site (www.dekunstmakers.com / dekunstmakers.com)

## Setup

1. Copy `.env.example` to `.env` and fill in your values
2. Start all services: `docker-compose up -d`
3. Check logs: `docker-compose logs -f`

## Deployment

### Initial Setup on Server

1. Copy `.env.example` to `.env` on the server at `/root/dekunstmakers/.env` and configure your environment variables
2. Run the GitHub Actions deployment workflow (it will copy `docker-compose.yml` and start services)

Alternatively, you can manually clone the repository and run `docker-compose up -d` locally on the server.

### Automated Deployment

This repository includes a GitHub Actions workflow for deploying infrastructure changes:

- **Manual only**: Triggered manually via GitHub Actions UI
- **Tag selection**: Optionally specify a tag to deploy, or leave empty to use the latest tag

The workflow will:
1. Checkout the specified tag (or latest tag if none provided)
2. Copy `docker-compose.yml` to the server
3. Pull latest images for all services
4. Apply changes with `docker-compose up -d`

**Required GitHub Secrets:**
- `SERVER_HOST`: Your server IP/domain
- `SSH_PRIVATE_KEY`: Private SSH key for server access

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

All services are on the `dekunstmakers-infra` bridge network, allowing them to communicate via service names.
