# Evolve-on-Click (EvOC) Full Stack Deployment

This directory contains the master `docker-compose.yml` file to deploy the entire EvOC application stack.

## Overview

The `docker-compose.yml` is configured to run all microservices, databases, and the frontend in a production-like environment. It uses pre-built Docker images from the [Evolutionary-Algorithms-On-Click GitHub Container Registry](https://github.com/orgs/Evolutionary-Algorithms-On-Click/packages).

The stack includes:
- `evolve_frontend`: The Next.js web application.
- `controller_v2`: The primary backend Go microservice.
- `auth`: The user authentication microservice.
- `llm_service`: The AI microservice for code generation.
- `jupyter_gateway` & `python_runner`: For executing notebook code.
- `runner_controller` & `runner`: For handling asynchronous background jobs.
- `cockroachdb`: The SQL database.
- `minio`: The S3-compatible object store.
- `redis`: The in-memory cache and message broker.

## Prerequisites

1.  **Docker and Docker Compose**: Ensure you have a recent version of Docker installed on your system.
2.  **Container Images**: All required container images must be built and pushed to the organization's GitHub Container Registry (`ghcr.io`). The compose file will pull these images.

## Setup

1.  **Create an Environment File**: This stack requires a number of environment variables and secrets to run. A template is provided in this directory. Copy the example file to a new `.env` file:
    ```bash
    cp .env.example .env
    ```

2.  **Configure Secrets**: Open the `.env` file and fill in all the required values, such as the `GROQ_API_KEY`, mailer passwords, and any other secrets.

## Running the Stack

Once your `.env` file is configured, you can start the entire application stack in detached mode:

```bash
docker compose up -d
```

This command will pull all the necessary images and start the services. You can view the logs for all running services with:

```bash
docker compose logs -f
```

## Stopping the Stack

To stop and remove all the running containers, use the following command:

```bash
docker compose down
```

To stop the containers without removing the underlying volumes (preserving your database and minio data), you can use:

```bash
docker compose stop
```