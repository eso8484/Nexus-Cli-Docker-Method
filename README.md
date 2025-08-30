# Nexus CLI Docker Setup

This repository contains a Dockerized setup for running multiple Nexus CLI nodes using Docker and Docker Compose.

## Prerequisites

* **Docker** installed on your system ([Install Docker](https://docs.docker.com/get-docker/))
* **Docker Compose** installed ([Install Docker Compose](https://docs.docker.com/compose/install/))

## Files Overview

* **Dockerfile**: Builds an Alpine-based image, installs the Nexus CLI using the official installation script.
* **docker-compose.yaml**: Defines multiple Nexus CLI containers, each running in headless mode with a unique node ID.

## Dockerfile

```dockerfile
FROM alpine:3.22.0

RUN apk update && \
    apk add curl && \
    curl -sSf https://cli.nexus.xyz/ -o install.sh && \
    chmod +x install.sh && \
    NONINTERACTIVE=1 ./install.sh

ENTRYPOINT ["/root/.nexus/bin/nexus-cli"]
```

## docker-compose.yaml

```yaml
services:
  nexus-cli-1:
    build: .
    container_name: nexus-cli-1
    command: ["start", "--headless", "--node-id", "replace-with-your-node-id-1"]

  nexus-cli-2:
    build: .
    container_name: nexus-cli-2
    command: ["start", "--headless", "--node-id", "replace-with-your-node-id-2"]

  nexus-cli-3:
    build: .
    container_name: nexus-cli-3
    command: ["start", "--headless", "--node-id", "replace-with-your-node-id-3"]
```

## Usage

1. **Clone the repository**:

```bash
git clone https://github.com/eso8484/Nexus-Cli-Docker-Method.git
cd Nexus-Cli-Docker-Method
```
### Pre-Req

1(a). **Download Nexus CLI**:
```bash
curl https://cli.nexus.xyz/ | sh
source ~/.bashrc
```
Register Node
```bash
source ~/.bashrc

nexus-network register-user --wallet-address your-wallet-address
```

2. **Build and start the containers**:

```bash
docker compose up -d --build
```

3. **Check container status**:

```bash
docker ps
```

4. **View logs for a specific container**:

```bash
docker logs nexus-cli-1
```

5. **Stop the containers**:

```bash
docker compose down
```

## Customization

* Update the `--node-id` values in `docker-compose.yaml` to match your own node IDs.
* Add or remove services as needed to run more or fewer nodes.

## Notes

* Ensure you have valid Nexus node IDs before running the containers.
* The setup uses Alpine Linux for a lightweight image.

## License

This project is provided as-is. Ensure compliance with Nexus CLI's terms of use.

