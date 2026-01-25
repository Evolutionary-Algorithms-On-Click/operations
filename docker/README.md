# Evolve-on-Click (EvOC) Full Stack Deployment & Development

This directory contains the master `docker-compose.yml`, developer-specific override files, and a `Makefile` to easily run the entire EvOC application stack.

## Overview: A Hybrid Approach

This setup uses a `Makefile` to simplify a hybrid Docker Compose approach.

-   **`docker-compose.yml` (Base File)**: Defines the entire stack using stable, pre-built images from the GitHub Container Registry.
-   **`docker-compose.<role>-dev.yml` (Override Files)**: Overrides a single service to build from local source code and enable live-reloading.
-   **`Makefile`**: Provides simple commands (`make up-backend`, `make down`, etc.) to manage the environment.

## Prerequisites

1.  **Make, Docker, and Docker Compose**: Ensure you have these tools installed.
2.  **Source Code**: You must have all project repositories (`controller_microservice_v2`, `evolve_frontend`, etc.) checked out in the same parent directory.

## One-Time Setup

Before you can run any services, you must create and configure your environment file.

1.  Navigate to this directory (`operations/docker`).
2.  Copy the example environment file:
    ```bash
    cp .env.example .env
    ```
3.  Open the `.env` file and fill in all required secrets (especially `GROQ_API_KEY`).

---

## Development & Operations Guide

All commands should be run from this directory (`operations/docker`).

### How to Start

Choose the command that matches your role:

-   **For Backend Development (`controller_v2`):**
    ```bash
    make up-backend
    ```
    *(This starts the full stack with live-reloading for the Go backend using `Air`.)*

-   **For Frontend Development (`evolve_frontend`):**
    ```bash
    make up-frontend
    ```
    *(This starts the full stack with live-reloading for the Next.js frontend.)*

-   **For LLM Service Development (`llm_service`):**
    ```bash
    make up-llm
    ```
    *(This starts the full stack with live-reloading for the Python LLM service.)*

-   **For Running the Stable Stack (QA / Testing):**
    ```bash
    make up
    ```
    *(This pulls all pre-built images from the registry without using any local code.)*

### General Management Commands

-   **Stop All Services:**
    ```bash
    make down
    ```

-   **Check Container Status:**
    ```bash
    make ps
    ```

-   **Follow Service Logs:**
    ```bash
    make logs service=<service_name>
    ```
    *Example: `make logs service=controller_v2`*

-   **See All Commands:**
    ```bash
    make help
    ```