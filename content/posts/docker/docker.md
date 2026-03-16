---
title: "DOCKER"
date: 2026-03-15
draft:  false
featured: false  
description: "DOCKER - Basics"
thumbnail: "/posts/docker/images/docker.png"
featureImage: "/posts/docker/images/docker.png"
shareImage: "/posts/docker/images/docker.png"
author: "Angel Vyas"
tags:
    - Docker
          
categories:     
    - DevOps
    - Docker
---


</br>

`Docker` is an open-source platform that allows developers to build, package, and run applications in containers. Containers are lightweight, standalone, and executable units that include everything needed to run a piece of software — including the code, runtime, libraries, and system tools.

Docker makes it easier to ensure that applications run consistently across different environments, such as development, testing, and production. It helps avoid the classic `"it works on my machine"` problem.

#### Key benefits of Docker:

**Portability**: Containers can run on any system that supports Docker.

**Efficiency**: Containers use system resources more efficiently than virtual machines.

**Speed**: Starting and stopping containers is faster than booting up full VMs.

**Isolation**: Applications run in isolated environments, improving security and reducing conflicts.

Docker is widely used in DevOps, cloud computing, microservices, and CI/CD pipelines.



</br>

🚀 **Docker Basics**

 | Command | Description |
 | :----| :---- |
 |docker --version or docker -v |Show installed Docker version|
 |docker info | Display system-wide info about Docker|
 |docker help or docker or docker --help|Show help for Docker commands|


### 🧱 **Docker Image**:
- A Docker image is like a `blueprint or template`.
- It contains everything needed to run an application: code, libraries, dependencies, and configurations.
- Think of it like a frozen `snapshot` of your app.

Example: An image might be based on Ubuntu, with Python and your app code installed.


📦 **Image Commands**
 # Docker Image Commands

| Command | Description |
|--------|-------------|
| `docker images` | List all Docker images |
| `docker image ls` | List all Docker images |
| `docker pull image_name` | Download an image from a registry |
| `docker build -t image_name .` | Build an image from a Dockerfile |
| `docker tag image_name username/repository:tag` | Tag an image for pushing to a registry |
| `docker push username/repository:tag` | Push an image to a registry |
| `docker rmi image_name` | Remove a Docker image |
| `docker rmi image_id` | Remove an image using its ID |
| `docker image inspect image_name` | Display detailed information about an image |
| `docker image history image_name` | Show the history of an image layers |
| `docker image prune` | Remove unused images |
| `docker save image_name -o file_name.tar` | Save an image to a tar archive |
| `docker load -i file_name.tar` | Load an image from a tar archive |
| `docker search image_name` | Search for an image in a registry |

**NOTE**
- . in docker build is to represent current directory.
- example of tagging an image: docker tag port-demo:latest port-demo:v1.
- To push images to Docker Hub, the image must be tagged in the format username/repository:tag. This associates the image with a Docker Hub repository so Docker knows where to push it.

### 📦 **Docker Container**:
- A Docker container is a `running instance of a Docker image`.
- It’s isolated, lightweight, and includes just what's needed to run your app.
- You can start, stop, restart, or delete containers anytime.

🧪 *Analogy*:
- Image = recipe
- Container = actual dish cooked from that recipe
 

🧱 **Container Commands**
# Docker Container Commands

| Command | Description |
|--------|-------------|
| `docker run image_name` | Create and start a container from an image |
| `docker run -d image_name` | Run a container in detached (background) mode |
| `docker run -it image_name` | Run a container interactively with a terminal |
| `docker run --name container_name image_name` | Run a container with a specific name |
| `docker ps` | List all running containers |
| `docker ps -a` | List all containers (running and stopped) |
| `docker stop container_name` | Stop a running container |
| `docker start container_name` | Start a stopped container |
| `docker restart container_name` | Restart a container |
| `docker kill container_name` | Force stop a container immediately |
| `docker rm container_name` | Remove a container |
| `docker rm -f container_name` | Force remove a running container |
| `docker logs container_name` | View logs of a container |
| `docker logs -f container_name` | Follow container logs in real time |
| `docker exec container_name command` | Execute a command inside a running container |
| `docker exec -it container_name bash` | Open an interactive bash shell inside a container |
| `docker attach container_name` | Attach the terminal to a running container |
| `docker inspect container_name` | Display detailed information about a container |
| `docker top container_name` | Show running processes inside a container |
| `docker stats` | Display live resource usage statistics of containers |
| `docker pause container_name` | Pause all processes in a container |
| `docker unpause container_name` | Resume a paused container |
| `docker rename old_container_name new_container_name` | Rename a container |
| `docker cp file_path container_name:/path` | Copy files between host and container |
| `docker port container_name` | Show port mappings of a container |
| `docker wait container_name` | Wait until a container stops and return exit code |


### **Docker Image Layers**
 Docker image is made up of a stack of layers, each representing a change or instruction from your Dockerfile.
 >📦 Think of layers like building blocks — each one stacks on top of the previous to form a complete image.

 🏗️ **How Docker Builds Layers**
When you build a Docker image using a Dockerfile, each line creates a new layer:
```Dockerfile
FROM ubuntu:20.04       # Layer 1 (base image)
RUN apt-get update      # Layer 2
RUN apt-get install -y python3 # Layer 3
COPY . /app              # Layer 4
CMD ["python3", "/app/app.py"] # Layer 5
```
💡 **Key Benefits of Layers**
|Feature | Description|
|:----|:----|
|Caching | Docker reuses unchanged layers to speed up builds|
|Storage Efficiency | Shared layers between images save disk space|
|Portability | Layers are versioned and distributed efficiently|
|Modularity | You can build images in small, manageable steps|


📁 **Where Are Layers Stored?**
- Layers are stored as separate read-only filesystems.

- When you run a container, Docker adds a read-write layer on top, so you can make changes without affecting the image.


🧼 **Layer Caching Tip**

To get the best use of Docker’s layer caching:
- Put least-changing instructions (like FROM, RUN apt-get) early in the Dockerfile
- Put frequently changing stuff (like COPY .) later.

### 🔌**Port Binding**
Port binding is how you connect your local machine (host) to the inside of a Docker container, so that services inside the container can be accessed from outside (like your browser or another app).

> Container port (internal) ↔ Host port (external)

📦 **Example:**
```bash
docker run -p 8080:80 nginx
```
🔍 `What it does`: </br>

Docker runs the NGINX container, which serves on port 80 (inside the container).

The -p 8080:80 flag maps:
- Host port 8080 → Container port 80

So you can now access the container at:
> 👉 http://localhost:8080

**COMMAND**
> docker run -p <host_port>:<container_port> image_name

💡 **Bonus Tip: Exposing vs Binding**

- `EXPOSE 80` in Dockerfile = The containerized app is expected to listen on port 80 (only for documentation purpose), It does not make the port accessible from the host machine.
- To access a container from the host machine, you must explicitly bind a host port to a container port using the -p flag when running the container.

</br>

###### `Important Rule for Port Binding`

A **host port can only be mapped to one container at a time**.  
If a container is already using a host port, another container cannot use the same host port.

Container 1: 8080 → 80 (works)</br>
Container 2: 8080 → 5000 (fails — port already in use)

To run multiple containers, use different host ports:

8080 → Container1:80</br>
8081 → Container2:80</br>
8082 → Container3:80</br>

Even if all containers use the same internal port, they can run simultaneously with different host ports.


### **Docker v/s VM**

- `Docker` = Think of it as a mini-app in a lightweight, isolated box that shares your computer’s OS.
- `VM` = Like running another full computer inside your computer (including its own OS, drivers, etc.).

✅ `When to Use Docker`:
- Fast, repeatable development
- CI/CD pipelines
- Running microservices
- Saving resources

✅ `When to Use VMs`:
- Running apps that require full OS isolation
- Need to simulate full environments
- Testing across different operating systems


🆚 **Docker vs Virtual Machine (VM)**

|Feature|	Docker (Containers)|	Virtual Machine (VM)|
|:----|:-----|:-----|
|Architecture|	Shares the host OS kernel|	Runs its own full OS|
|Boot Time|	Seconds|	Minutes|
|Resource Usage	|Lightweight|	Heavy (more CPU/RAM)|
|Size	|MBs (tiny)	|GBs (huge)|
|Isolation|	Process-level|	OS-level (stronger isolation)|
|Performance|	Near-native speed|	Slower due to overhead|
|Portability|	Highly portable	|Less portable|
|Use Case	|Microservices, DevOps, CI/CD|	Full OS testing, Legacy apps|


### **Docker Network**

🌐 **What is Docker Networking?**

Docker networking lets containers communicate:

- With each other
- With the host system
- With the outside world (internet)

Just like real computers, containers need IP addresses, ports, and rules to talk to one another.

**COMMANDS**
# Docker Network Commands

| Command | Description |
|--------|-------------|
| `docker network ls` | List all Docker networks |
| `docker network create network_name` | Create a new Docker network |
| `docker network inspect network_name` | Display detailed information about a network |
| `docker network connect network_name container_name` | Connect a container to a network |
| `docker network disconnect network_name container_name` | Disconnect a container from a network |
| `docker network rm network_name` | Remove a Docker network |
| `docker network prune` | Remove all unused networks |
| `docker network create --driver bridge network_name` | Create a bridge network |
| `docker network create --driver host network_name` | Create a host network |
| `docker network create --driver overlay network_name` | Create an overlay network for multi-host communication |

### **Docker Compose**
Docker Compose is a tool that lets you define and run `multi-container` Docker applications easily using a simple `YAML configuration` file.

📦 **What It Does**:
Instead of starting each container one by one with docker run, Docker Compose lets you:
- Define all your services (e.g., app, database, cache, image, ports, etc) in one file.
- Start everything with a single command:

```bash
docker-compose up
```

🛠️ Example:
Let’s say you have mongo container and a mongo-express container. Here's what a docker-compose.yml file might look like:
```bash
version: '3.8'

services:
  mongo:
    image: mongo
    container_name: mongo
    networks:
      - mongo-network
    environment:
      - MONGO_INITDB_ROOT_USERNAME=angel
      - MONGO_INITDB_ROOT_PASSWORD=123456
    ports:
      - "27017:27017"
    volumes:
      - mongo-data:/data/db

  mongo-express:
    image: mongo-express
    container_name: mongo-express
    networks:
      - mongo-network
    environment:
      - ME_CONFIG_MONGODB_ADMINUSERNAME=angel
      - ME_CONFIG_MONGODB_ADMINPASSWORD=123456
      - ME_CONFIG_MONGODB_URL=mongodb://admin:qwerty@mongo:27017/?authSource=admin
      - ME_CONFIG_BASICAUTH_USERNAME=admin
      - ME_CONFIG_BASICAUTH_PASSWORD=qwerty
    ports:
      - "8081:8081"

networks:
  mongo-network:
    driver: bridge

volumes:
  mongo-data:
  ```
✅ Key Benefits:
- Simplifies multi-container setups
- Easy to share and reuse using the docker-compose.yml file
- Supports networking, volumes, and environment configs
- Great for local development and testing

**COMMANDS**

| **Command**                            | **Description**                                                      |
| -------------------------------------- | -------------------------------------------------------------------- |
| `docker-compose up`                    | Builds (if needed) and starts all services defined in the YAML file. |
| `docker-compose up -d`                 | Starts all services in **detached** (background) mode.               |
| `docker-compose down`                  | Stops and removes all running containers, networks, and volumes.     |
| `docker-compose build`                 | Builds images for all services without starting the containers.      |
| `docker-compose up --build`            | Forces rebuild of images, then starts services.                      |
| `docker-compose restart`               | Restarts all the running containers.                                 |
| `docker-compose logs`                  | Shows logs from all containers.                                      |
| `docker-compose logs [service]`        | Shows logs for a specific service (e.g., `logs web`).                |
| `docker-compose ps`                    | Lists the status of all containers defined in the YAML file.         |
| `docker-compose down --volumes`        | Removes containers **and volumes**.                                  |
| `docker-compose down --remove-orphans` | Removes orphaned containers not defined in the YAML file.            |


### **Docker Volumes**
A Docker volume is a special storage mechanism that lets containers store data persistently, even after the container is deleted or restarted.

🧠 **Why Use Volumes?**
-`Persistence`: Data is not lost when a container stops or is removed.
-`Sharing`: Multiple containers can access the same volume.
-`Separation`: Keeps application data separate from container logic.
-`Backups`: Volumes can be easily backed up and restored.

🛠️ **Common Volume Commands**
| Command                       | Description                        |
| ----------------------------- | ---------------------------------- |
| `docker volume create myvol`  | Creates a new volume named `myvol` |
| `docker volume ls`            | Lists all volumes                  |
| `docker volume inspect myvol` | Shows details about a volume       |
| `docker volume rm myvol`      | Deletes a volume                   |
| `docker volume prune`         | Deletes all unused volumes         |

📦 **Using Volumes in docker run**
```bash
docker run -v myvol:/app/data myimage
```

🧱 **Types of Docker Storage**
| Type            | Description                                    | Use Case                                  |
| --------------- | ---------------------------------------------- | ----------------------------------------- |
| **Volumes**     | Managed by Docker in `/var/lib/docker/volumes` | Most recommended for persistent data      |
| **Bind Mounts** | Maps a specific host path to a container       | When you need control over the exact path |
| **tmpfs**       | Stores data in memory only (temporary)         | For sensitive or fast access data         |

# Docker Fundamentals

## Hypervisor
A **hypervisor** is the layer that virtualizes hardware so multiple operating systems can run on the same physical machine.

It allows multiple virtual machines to share the same hardware resources.

---

## Containers and the OS Kernel

Containers contain **user-space parts of an operating system**, but **not the kernel**.

This means containers include things like:

- Application code
- Libraries
- Dependencies
- System utilities

However, they **do not include their own kernel**.

---

## Container Runtime

A **container runtime** like Docker is responsible for creating and running containers.

Containers include:

- The application
- Dependencies
- User-space OS components

But **kernel-level operations are handled by the host machine’s operating system**.

So the container runtime manages containers while the **host OS kernel executes system calls**.

---

## What Actually Runs in a Container

When you run:

```bash
docker run ubuntu
```

You might think:

> "Ubuntu OS is running inside the container."

But in reality:

- Only **Ubuntu user-space tools** are running.
- The **kernel is still the host machine's kernel**.

So the container is **not running a full operating system**.

---

## Docker with WSL Integration

When **WSL integration is enabled**, Docker Desktop runs the **Docker Engine inside a WSL2 virtual machine (`docker-desktop`)**.

This VM provides the **Linux kernel required for containers**.

---

## Linux Kernel Requirement

Regardless of whether Docker uses **WSL2** or **Hyper-V**:

❗ **Containers always require a Linux kernel.**

Since Windows does not have a Linux kernel, Docker must run a **Linux virtual machine**.

This can be provided by:

- **WSL2 VM**
- **Hyper-V VM**

---

## Relationship Between WSL2 and Docker

The relationship between these components is:

- **WSL2 → Provides the Linux OS environment**
- **Docker → Runs isolated applications (containers) inside that OS**

Architecture example:

```
Hardware
   ↑
Windows
   ↑
WSL2 (Linux Kernel)
   ↑
Docker Engine
   ↑
Containers
```

Containers then run as **isolated processes sharing the same Linux kernel**.





