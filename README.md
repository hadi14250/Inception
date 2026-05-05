
<div align="center">
<a href="https://github.com/hadi14250">
    <img src="github_gifs/docker.gif" alt="3d cube" width="150" height="150">
  </a>
  <h3 align="center">Inception</h3>
  System administration exercise with Docker to manage and configure services
  <br>
</div>

<br>

# Inception

**Inception** is a 42 system administration project that introduces containerization with Docker. The goal is to build a small infrastructure of services running inside a virtual machine — each service in its own container, wired together through Docker Compose.

The stack runs three services behind a single TLS entry point: **NGINX** terminates HTTPS on port 443, **WordPress + PHP-FPM** serves the site, and **MariaDB** stores the data. All three images are built from scratch on the penultimate stable version of Debian or Alpine — no pre-built application images from Docker Hub.

<br>

## Stack

| Service | Role | Notes |
| --- | --- | --- |
| **NGINX** | Reverse proxy / TLS termination | Only exposed port is **443**, TLSv1.2 / TLSv1.3 only |
| **WordPress + PHP-FPM** | Application layer | Talks to NGINX over FastCGI on the internal network |
| **MariaDB** | Database backend | Isolated on the internal Docker network |
| **Docker Compose** | Orchestration | Defines services, network, and volumes |
| **Docker volumes** | Persistence | Bind-mounted to `/home/${USER}/data` so state survives restarts |

<br>

## Requirements

- Docker and the Docker daemon running
- `docker-compose`
- `make`

<br>

## How to run

From the project root:

```sh
make        # build images and start containers in detached mode
make clean  # stop containers, remove images and volumes from the compose file
make fclean # full clean — also wipes bind-mounted data and prunes volumes
make re     # rebuild from a clean state
```

<br>

## Project Structure

<div align="center">
<a href="https://github.com/hadi14250">
    <img src="github_gifs/structure.png" alt="3d cube" width="500" height="500">
  </a>
  <br>
  <br>
</div>
