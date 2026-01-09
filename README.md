# EvOC Operations (Infrastructure & DevOps)

Welcome to the **operations** repository for **EvOC (Evolutionary Algorithms on Click)**. This repository contains all the configuration files, automation scripts, and deployment manifests required to set up and manage the EvOC infrastructure across different environments.

## Overview

This repository is designed to automate the deployment of the EvOC microservices architecture. It supports a robust, production-ready environment using Kubernetes and Ansible, while maintaining a simple Docker Compose setup for local development.

### Key Features
- **Automated Kubernetes Deployment**: Full lifecycle management (init/join) of a multi-node K8s cluster.
- **CRI-Dockerd Integration**: Seamlessly bridges Kubernetes with Docker Engine (v0.3.21) for reliable container orchestration.
- **Architecture Aware**: Automatic detection and support for both `amd64` and `arm64` (Apple Silicon) architectures.
- **Infrastructure-as-Code (IaC)**: Ansible playbooks for automated provisioning of CockroachDB, MinIO, RabbitMQ, and Kubernetes components.
- **Microservices Orchestration**: Pre-configured Kubernetes manifests for the Auth, Runner, Frontend, and Controller services.

---

## Repository Structure

| Directory | Description |
|-----------|-------------|
| [`/ansible`](./ansible) | Ansible playbooks and inventory for server-side automation and cluster setup. |
| [`/kubernetes`](./kubernetes) | K8s manifests (Deployments, Services, Secrets) for microservice orchestration. |
| [`/docker`](./docker) | Docker Compose configurations for quick local development. |

---

## Prerequisites

Before starting, ensure you have the following tools installed on your local machine:
- [Ansible CLI](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- [Docker Engine](https://docs.docker.com/get-docker/)
- [SSH Access](https://www.ssh.com/academy/ssh/public-key-authentication) to target nodes.

---

## Quick Start

### 1. Local Development (Docker Compose)
For a quick local setup, navigate to the `docker` directory and follow the instructions in its README.
```bash
cd docker
docker-compose up -d
```

### 2. Multi-Node Production Cluster (Ansible + K8s)
For setting up a full production-ready cluster, refer to the [Ansible README](./ansible/README.md).
1. Configure your nodes in `ansible/inventory.ini`.
2. Define your secrets in `ansible/vars/`.
3. Run the playbook:
```bash
cd ansible
ansible-playbook -i inventory.ini playbook.yaml -kK
```

---

## Security & Secrets

Sensitive information (API keys, database credentials) are managed via:
- **Ansible Vars**: Stored in `ansible/vars/` (excluded from Git).
- **K8s Secrets**: Defined in `kubernetes/evolve-secrets.yaml`.

*Always ensure your local secrets files are excluded from version control.*

---

## Contributing
Please follow the standard Git workflow:
1. Fork the repo.
2. Create your feature branch (`git checkout -b feature/amazing-feature`).
3. Commit your changes (`git commit -m 'Add some amazing feature'`).
4. Push to the branch (`git push origin feature/amazing-feature`).
5. Open a Pull Request.
