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
    - general
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


### 🧱 **Docker Image**:
- A Docker image is like a `blueprint or template`.
- It contains everything needed to run an application: code, libraries, dependencies, and configurations.
- Think of it like a frozen `snapshot` of your app.

Example: An image might be based on Ubuntu, with Python and your app code installed.


### 📦 **Docker Container**:
- A Docker container is a `running instance of a Docker image`.
- It’s isolated, lightweight, and includes just what's needed to run your app.
- You can start, stop, restart, or delete containers anytime.

🧪 *Analogy*:
- Image = recipe
- Container = actual dish cooked from that recipe