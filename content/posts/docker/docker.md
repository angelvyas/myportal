---
title: "DOCKER"
date: 2025-04-19
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
s
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
  | Command | Description |
 | :----| :---- |
|docker pull <image_name>|	Download an image from Docker Hub|
|docker build -t <name> .|	Build an image from a Dockerfile in current dir|
|docker imagses|	List all local images|
|docker rmi <image>|	Remove an image|
|docker tag <src> < target>|	Tag an image for a repo|
|docker push <image_name>|	Push image to Docker Hub or registry|  



### 📦 **Docker Container**:
- A Docker container is a `running instance of a Docker image`.
- It’s isolated, lightweight, and includes just what's needed to run your app.
- You can start, stop, restart, or delete containers anytime.

🧪 *Analogy*:
- Image = recipe
- Container = actual dish cooked from that recipe
 

🧱 **Container Commands**
|Command|	Description|
|:----|:------|
|docker run <image>|	Run a container from image|
|docker run -it <image>|	Interactive terminal|
|docker run -d <image>|	Run in background (detach mode)|
|docker run --name <name> <image>|	Assign a name to the container|
|docker ps|	List running containers|
|docker ps -a|	List all containers|
|docker stop <container>|	Stop a running container|
|docker start <container>|	Start a stopped container|
|docker restart <container>|	Restart a container|
|docker rm <container>|	Remove a container|
|docker exec -it <container_id> bash|	Run command inside a container|
|docker logs <container>|	View container logs|


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
🔍 `What it does`:
Docker runs the NGINX container, which serves on port 80 (inside the container).

The -p 8080:80 flag maps:
- Host port 8080 → Container port 80

So you can now access the container at:
> 👉 http://localhost:8080

**COMMAND**
> docker run -p <host_port>:<container_port> <image>

💡 **Bonus Tip: Exposing vs Binding**

EXPOSE 80 in Dockerfile = suggests the container listens on port 80.
- But only -p actually binds it to the host for access.

NOTE: if for eg host port 8080 is ported with the container port 3306, then the host port now cannot connect to any other containers port now, only one port binding at a time between host port and container port.

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
|Command|	Description|
|:----|:----|
|docker network ls|	List all networks|
|docker network inspect <network_name>|	Show network details (IP ranges, connected containers)|
|docker network create <network_name>|	Create a custom network|
|docker network rm <network_name>|	Remove a network|
|docker network connect <network_name> <container_name>	|Add container to a network|
|docker network disconnect <netwok_name> <container_name>|	Remove container from network|