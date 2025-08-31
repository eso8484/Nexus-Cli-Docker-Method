# Nexus CLI Docker Setup

This repository contains a Dockerized setup for running multiple Nexus CLI nodes using Docker and Docker Compose.

## Prerequisites

* **Docker** installed on your system ([Install Docker](https://docs.docker.com/get-docker/))
* **Docker Compose** installed ([Install Docker Compose](https://docs.docker.com/compose/install/))

## Files Overview

* **Dockerfile**: Builds an Alpine-based image, installs the Nexus CLI using the official installation script.
* **docker-compose.yaml**: Defines multiple Nexus CLI containers, each running in headless mode with a unique node ID.

---

## --> Create account
* Create an account at https://app.nexus.xyz.

* Follow the account linking instructions.

* Your contributions will earn NEX Points.

* Track your progress on the leaderboard.

* Manage all your nodes in one place.
---

### 1. Install Dependecies
```bash
sudo apt update & sudo apt upgrade -y
sudo apt install screen curl build-essential pkg-config libssl-dev git-all -y
sudo apt install protobuf-compiler -y
sudo apt update
```
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
```bash
source $HOME/.cargo/env
```
```bash
rustup target add riscv32i-unknown-none-elf

```

  
## Usage

1. **Clone the repository**:

```bash
git clone https://github.com/eso8484/Nexus-Cli-Docker-Method.git
cd Nexus-Cli-Docker-Method
```
1(a). 
```bash
nana docker-compose.yaml
```
* Replace `Replace-with-actual-Node-ID` with your `node-ID` from the site then press `ctrl + o`, hit enter, then `ctrl + x`.
  
2. **Build and start the containers**:
2(a). * **Buld**

```bash
docker compose build --no-cache
```
2(b). **Check Image name for Nexus**
```bash
sudo docker images
```
---

**Register Node**
- Note: Replace `my_nexus_image` and `your-wallet-address` with  your `image name` from step 2(b) above and `evm wallet address` respectively in the next command before you run it
```bash
source ~/.bashrc
docker run --rm my_nexus_image /root/.nexus/bin/nexus-network register-user --wallet-address <your-wallet-address>
```

* **Run**
```bash
docker compose up -d 
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

