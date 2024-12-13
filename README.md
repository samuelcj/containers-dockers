# Understanding Containerization Technology Using Dockers

This README provides a comprehensive guide on containerization technology using Docker, including installation, basic commands, and practical implementations such as connecting applications with databases and managing Docker networks, volumes, and registries.

---

## Table of Contents

1. [What is a Container?](#what-is-a-container)
2. [Container Repository](#container-repository)
3. [Technical Overview](#technical-overview)
4. [Installing Docker](#installing-docker)
5. [Basic Docker Commands](#basic-docker-commands)
6. [Containers vs Images](#containers-vs-images)
7. [Docker Architecture](#docker-architecture)
8. [OS vs VirtualBox vs Docker](#os-vs-virtualbox-vs-docker)
9. [Using Docker Compose](#using-docker-compose)
10. [Dockerfile Overview](#dockerfile-overview)
11. [Docker Registry](#docker-registry)
12. [Deploying Applications](#deploying-applications)
13. [Docker Volumes](#docker-volumes)
14. [Running Nexus as a Docker Container](#running-nexus-as-a-docker-container)

---

## What is a Container?
A container is a way to package applications with all necessary dependencies and configurations. It provides an isolated operating system layer, enabling developers to avoid dependency conflicts and environmental configuration issues.

---

## Container Repository
A container repository is a storage system for container images. Examples include Docker Hub, a public repository for Docker images.

---

## Technical Overview
- Containers allow multiple versions of the same application to run without conflicts.
- They eliminate the need for pre-configured environments on servers, requiring only Docker Runtime to be set up.
- Docker is the most popular container implementation, with others like Containerd and CRI-O.

---

## Installing Docker
Follow the official guide for Ubuntu installation: [Docker Installation Guide](https://docs.docker.com/engine/install/ubuntu/).

Verify the installation using:
```
docker --version
```

---

## Basic Docker Commands
### Pulling Images
```bash
docker pull <image_name>
docker pull <image_name>:<version>
```
Example:
```bash
docker pull postgres
```
### Running Containers
```bash
docker run <image_name>
docker run -d <image_name>
```
### Listing Images and Containers
```bash
docker images
docker ps
docker ps -a
```
### Managing Containers
```bash
docker stop <container_id>
docker start <container_id>
```
### Accessing Logs
```bash
docker logs <container_id>
docker logs <container_name>
```
For more commands, refer to the section on [Docker Basic Commands](#docker-basic-commands).

---

## Containers vs Images
- **Image**: A packaged, non-running container consisting of the application, dependencies, and configurations.
- **Container**: A running instance of an image.

---

## Docker Architecture
Docker Engine comprises three main components:
1. **Docker Server**: Manages images and containers.
2. **Docker API**: Interfaces with the server.
3. **Docker CLI**: Executes commands.

---

## OS vs VirtualBox vs Docker
- **OS**: Comprises the Kernel and Application layers.
- **Docker**: Virtualizes the Application layer and uses the host OS Kernel.
- **Virtual Machines**: Virtualize both Kernel and Application layers.

---

## Using Docker Compose
Docker Compose allows you to run multiple containers using a YAML configuration file. Example:

```yaml
version: "3.8"
services:
  app:
    image: my-app
    ports:
      - "3000:3000"
  db:
    image: postgres
    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: password
```
Run the compose file with:
```bash
docker-compose -f docker-compose.yml up
```

---

## Dockerfile Overview
A Dockerfile defines the blueprint for building images. Key commands include:
- `FROM`: Specifies the base image.
- `RUN`: Executes Linux commands inside the container.
- `CMD`: Specifies the command to run when the container starts.

Example:
```dockerfile
FROM node:13-alpine
WORKDIR /app
COPY . .
RUN npm install
CMD ["node", "server.js"]
```
Build an image with:
```bash
docker build -t my-image .
```

---

## Docker Registry
Store and retrieve Docker images from registries such as AWS ECR or Docker Hub. Example:
```bash
docker push <repository_url>/<image_name>:<tag>
```

---

## Deploying Applications
1. Pull necessary images (e.g., MongoDB, Mongo Express).
2. Create a Docker network:
```bash
docker network create my-network
```
3. Run containers in the network.

---

## Docker Volumes
Volumes ensure data persistence for containers. Examples:
- Named Volume:
```bash
docker volume create --name my-volume
```
- Host Volume:
```bash
docker run -v /host/path:/container/path <image_name>
```

---

## Running Nexus as a Docker Container
1. Create a named volume:
```bash
docker volume create nexus-data
```
2. Run the Nexus container:
```bash
docker run -d -p 8081:8081 --name nexus -v nexus-data:/sonatype-work sonatype/nexus
```

---

Containers are beautiful tools in making deployment easy. This is the way to go as a DevOps engineer!!!

