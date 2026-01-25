# Makefile for EvOC Development Environment
# See 'make help' for a list of commands.

# Default command
.DEFAULT_GOAL := help

# Use shell functions to get service name for logs
# Usage: make logs service=<service-name>
service = $(filter-out $@,$(MAKECMDGOALS))

.PHONY: help up up-backend up-frontend up-llm down ps logs

help:
	@echo "------------------------------------------------------------------------"
	@echo " EvOC Development Environment Makefile"
	@echo "------------------------------------------------------------------------"
	@echo "Usage: make <command>"
	@echo ""
	@echo "Development Commands:"
	@echo "  up-backend        Starts the full stack with LIVE-RELOADING for the Backend."
	@echo "  up-frontend       Starts the full stack with LIVE-RELOADING for the Frontend."
	@echo "  up-llm            Starts the full stack with LIVE-RELOADING for the LLM Service."
	@echo ""
	@echo "General Commands:"
	@echo "  up                Starts the full STABLE stack using pre-built images."
	@echo "  down              Stops and removes all services."
	@echo "  ps                Shows the status of all running containers."
	@echo "  logs service=<name> Follows the logs for a specific service (e.g., 'make logs service=controller_v2')."
	@echo ""

up:
	@echo "Starting STABLE stack from pre-built images..."
	docker compose -f docker-compose.yml up -d

up-backend:
	@echo "Starting stack for BACKEND development..."
	docker compose -f docker-compose.yml -f docker-compose.backend-dev.yml up -d --build

up-frontend:
	@echo "Starting stack for FRONTEND development..."
	docker compose -f docker-compose.yml -f docker-compose.frontend-dev.yml up -d --build

up-llm:
	@echo "Starting stack for LLM development..."
	docker compose -f docker-compose.yml -f docker-compose.llm-dev.yml up -d --build

down:
	@echo "Stopping all services..."
	docker compose down --remove-orphans

ps:
	docker compose ps

logs:
ifndef service
	@echo "ERROR: Missing 'service' argument. Usage: make logs service=<service-name>"
	@exit 2
else
	docker compose logs -f $(service)
endif
