# 🐳 Complete Docker Mastery Guide: Zero to Job-Ready

> **A comprehensive, progressive learning path from Docker fundamentals to production-ready deployments**

---

## 📚 Quick Navigation

### 🎯 Learning Phases
- [Phase 1: Foundations (Week 1-2)](#phase-1-foundations-week-1-2)
- [Phase 2: Core Docker Skills (Week 3-4)](#phase-2-core-docker-skills-week-3-4)

### 📖 Complete Topic Index

**Phase 1: Foundations**
1. [What is Docker and Why It Is Used](#1-what-is-docker-and-why-it-is-used)
2. [Virtual Machines vs Containers](#2-virtual-machines-vs-containers)
3. [Docker Architecture](#3-docker-architecture)
4. [Docker Installation (Linux-based)](#4-docker-installation-linux-based)

**Phase 2: Core Docker Skills**
5. [Linux Users in Docker Context](#5-linux-users-in-docker-context)
6. [Docker Images Deep Dive](#6-docker-images-deep-dive)
7. [Docker Containers Deep Dive](#7-docker-containers-deep-dive)
8. [Dockerfile Mastery (Very Important)](#8-dockerfile-mastery-very-important)

---

## PHASE 1: FOUNDATIONS (Week 1-2)

### 1. What is Docker and Why It Is Used

#### 💡 Simple Explanation
Imagine you built a website on your laptop. It works perfectly. But when you try to run it on a server, it breaks because:
- Different operating system
- Missing libraries
- Wrong software versions

**Docker solves this** by packaging your application + all its dependencies into a **container** that runs the same way everywhere.

#### 🎓 Professional Depth

Docker is a **containerization platform** that allows you to:
1. **Package** applications with all dependencies
2. **Ship** them as lightweight, portable units
3. **Run** them consistently across any environment

#### 🎯 Why Docker is Used

| Benefit | Description |
|---------|-------------|
| **Consistency** | "It works on my machine" problem solved |
| **Isolation** | Applications don't interfere with each other |
| **Speed** | Start applications in seconds (vs minutes for VMs) |
| **Efficiency** | Share OS kernel, use fewer resources |
| **Scalability** | Easy to replicate and scale |
| **DevOps Integration** | Perfect for CI/CD pipelines |

#### 🌍 Real-World Use Cases
- Microservices architecture
- CI/CD pipelines
- Local development environments
- Cloud deployments
- Testing different software versions

---

### 2. Virtual Machines vs Containers

#### 💡 Simple Explanation

**Virtual Machine (VM):**
- Like having multiple complete computers inside one computer
- Each has its own operating system
- Heavy and slow to start

**Container:**
- Like having multiple apartments in one building
- All share the same foundation (OS kernel)
- Lightweight and fast to start

#### 📊 Professional Comparison

| Aspect | Virtual Machine | Container |
|--------|----------------|-----------|
| **OS** | Full OS per VM | Shares host OS kernel |
| **Size** | GBs (gigabytes) | MBs (megabytes) |
| **Startup** | Minutes | Seconds |
| **Resource Usage** | Heavy | Lightweight |
| **Isolation** | Complete | Process-level |
| **Portability** | Limited | Highly portable |

#### 🏗️ Architecture Comparison

**VIRTUAL MACHINE:**
```
┌─────────────────────────────────┐
│     App A   │    App B          │
│  ┌────────┐ │ ┌────────┐        │
│  │ Bins/  │ │ │ Bins/  │        │
│  │ Libs   │ │ │ Libs   │        │
│  └────────┘ │ └────────┘        │
│  Guest OS   │  Guest OS         │
├─────────────┴──────────────────┤
│        Hypervisor               │
├─────────────────────────────────┤
│        Host OS                  │
├─────────────────────────────────┤
│        Hardware                 │
└─────────────────────────────────┘
```

**CONTAINER:**
```
┌─────────────────────────────────┐
│  App A   │   App B   │  App C   │
│ ┌──────┐ │ ┌──────┐  │ ┌──────┐│
│ │Bins/ │ │ │Bins/ │  │ │Bins/ ││
│ │Libs  │ │ │Libs  │  │ │Libs  ││
│ └──────┘ │ └──────┘  │ └──────┘│
├──────────┴───────────┴─────────┤
│      Docker Engine              │
├─────────────────────────────────┤
│        Host OS                  │
├─────────────────────────────────┤
│        Hardware                 │
└─────────────────────────────────┘
```

#### ⚖️ When to Use What

**Use VMs when:**
- You need complete OS isolation
- Different OS types required
- Strong security boundaries needed

**Use Containers when:**
- Building microservices
- Implementing DevOps practices
- Developing cloud-native apps
- Need rapid scaling

---

### 3. Docker Architecture

#### 💡 Simple Explanation

Docker works like a restaurant:
- **Docker Client** = Customer (you give orders)
- **Docker Daemon** = Kitchen (does the cooking)
- **Docker Registry** = Grocery Store (where ingredients come from)

#### 🏗️ Professional Architecture

Docker uses a **client-server architecture**:

```
┌──────────────┐
│ Docker Client│ (CLI: docker run, docker build, etc.)
└──────┬───────┘
       │ REST API
       ↓
┌──────────────────────────────────────┐
│     DOCKER DAEMON (dockerd)          │
│                                      │
│  ┌────────────────────────────────┐ │
│  │   Container Management         │ │
│  │   Image Management             │ │
│  │   Network Management           │ │
│  │   Volume Management            │ │
│  └────────────────────────────────┘ │
└──────────────┬───────────────────────┘
               │
               ↓
       ┌───────────────┐
       │ Docker Registry│ (Docker Hub, private registry)
       └───────────────┘
```

#### 🔧 Key Components

**1. Docker Client (`docker` CLI)**
- Interface you interact with
- Sends commands to Docker Daemon
- Can connect to remote daemons

**2. Docker Daemon (`dockerd`)**
- Background service running on host
- Manages Docker objects (images, containers, networks, volumes)
- Listens for Docker API requests
- Can communicate with other daemons

**3. Docker Registry**
- Stores Docker images
- **Docker Hub**: Public registry (default)
- **Private registries**: AWS ECR, Google GCR, Azure ACR, self-hosted

**4. Docker Objects**
- **Images**: Read-only templates
- **Containers**: Runnable instances of images
- **Networks**: Communication between containers
- **Volumes**: Persistent data storage

#### ⚙️ How It Works

**Example workflow:**
```bash
$ docker run nginx

1. Docker Client sends command to Docker Daemon
2. Daemon checks if 'nginx' image exists locally
3. If not, pulls from Docker Hub
4. Creates a container from the image
5. Starts the container
```

---

### 4. Docker Installation (Linux-based)

#### 📦 For Ubuntu/Debian

```bash
# 1. Update package index
sudo apt-get update

# 2. Install prerequisites
sudo apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

# 3. Add Docker's official GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# 4. Set up stable repository
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# 5. Install Docker Engine
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin

# 6. Verify installation
sudo docker run hello-world

# 7. Add your user to docker group (to run without sudo)
sudo usermod -aG docker $USER

# 8. Log out and log back in, then test
docker run hello-world
```

#### 📦 For CentOS/RHEL

```bash
# 1. Remove old versions
sudo yum remove docker docker-client docker-client-latest docker-common docker-latest docker-latest-logrotate docker-logrotate docker-engine

# 2. Set up repository
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

# 3. Install Docker Engine
sudo yum install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin

# 4. Start Docker
sudo systemctl start docker
sudo systemctl enable docker

# 5. Verify
sudo docker run hello-world
```

#### ✅ Post-Installation Verification

```bash
# Check Docker version
docker --version
docker version

# Check Docker info
docker info

# Check Docker Compose
docker compose version
```

---

## PHASE 2: CORE DOCKER SKILLS (Week 3-4)

### 5. Linux Users in Docker Context

#### 💡 Simple Explanation

Just like your computer has user accounts (admin vs regular user), Docker containers also run with specific users for security.

#### 👥 Linux User Types

**1. Root User (UID 0)**
- Superuser with all privileges
- Can do anything on the system
- ⚠️ Security risk if compromised

**2. Normal User (UID ≥ 1000)**
- Your regular user account
- Limited privileges
- ✅ Safer for everyday tasks

**3. System User (UID 1-999)**
- Used by services/daemons
- Examples: `www-data`, `mysql`, `nginx`
- No login shell typically

#### 🔐 Docker User & Group

```bash
# Docker group created during installation
getent group docker
# Output: docker:x:999:your-username

# Why add user to docker group?
# Without it, you need sudo for every docker command
sudo docker ps    # Without group membership
docker ps         # With group membership
```

#### 🔍 Users in Docker Images

Every Docker image has a default user (usually root). You can check:

```bash
# Check user in an image
docker run --rm nginx whoami
# Output: root

docker run --rm node:alpine whoami
# Output: node (non-root user)
```

#### 🎯 Why Docker Uses Users in Images

1. **Security**: Limit what container processes can do
2. **Principle of Least Privilege**: Only give necessary permissions
3. **Host Protection**: If container is compromised, attacker has limited access

#### 🛡️ Security Best Practices

**❌ Bad Practice (Running as Root):**
```dockerfile
FROM ubuntu:22.04
# Runs as root by default
COPY app.js /app/
CMD ["node", "/app/app.js"]
```

**✅ Good Practice (Non-Root User):**
```dockerfile
FROM ubuntu:22.04

# Create a non-root user
RUN groupadd -r appuser && useradd -r -g appuser appuser

# Set working directory
WORKDIR /app

# Copy files
COPY app.js /app/

# Change ownership
RUN chown -R appuser:appuser /app

# Switch to non-root user
USER appuser

CMD ["node", "app.js"]
```

#### 🚀 Running Containers as Non-Root

```bash
# Method 1: Specify user at runtime
docker run --user 1000:1000 nginx

# Method 2: Use USER instruction in Dockerfile
# (shown above)

# Method 3: Check what user container is running as
docker exec <container-id> whoami
```

#### 💼 Real-World Security Scenario

```dockerfile
# Example: Node.js application with security best practices
FROM node:18-alpine

# Create app directory
WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies as root (needed for npm)
RUN npm ci --only=production

# Copy application files
COPY . .

# Create non-root user
RUN addgroup -g 1001 -S nodejs && \
    adduser -S nodejs -u 1001

# Change ownership of app files
RUN chown -R nodejs:nodejs /app

# Switch to non-root user
USER nodejs

# Expose port
EXPOSE 3000

CMD ["node", "server.js"]
```

#### ⚠️ Common Security Mistakes

**1. Running as root unnecessarily**
```bash
# Bad: Allows full system access
docker run -d --privileged nginx
```

**2. Mounting sensitive host paths**
```bash
# Dangerous: Exposes host filesystem
docker run -v /:/host ubuntu
```

**3. Not using USER instruction**
- Always specify a non-root user in production images

#### 🔍 Checking Container User

```bash
# See what user a container runs as
docker inspect <container-id> | grep -i user

# Execute command as specific user
docker exec -u root <container-id> whoami
```

---

### 6. Docker Images Deep Dive

#### 💡 Simple Explanation

A Docker image is like a recipe + ingredients for your application. It contains:
- Operating system files
- Your application code
- Dependencies and libraries
- Configuration files

#### 🎓 Professional Depth

**What is a Docker Image?**

A Docker image is a **read-only template** containing:
1. Base OS (Ubuntu, Alpine, etc.)
2. Application runtime (Node.js, Python, Java)
3. Application code
4. Dependencies
5. Configuration
6. Metadata

#### 🧱 Image Layers and UnionFS

Docker images are built in **layers** using a **Union File System**:

```
┌─────────────────────────────┐
│  Layer 4: CMD ["npm start"] │  <-- Metadata layer
├─────────────────────────────┤
│  Layer 3: COPY . /app       │  <-- Your app code
├─────────────────────────────┤
│  Layer 2: RUN npm install   │  <-- Dependencies
├─────────────────────────────┤
│  Layer 1: FROM node:18      │  <-- Base image
└─────────────────────────────┘
```

**Key Concepts:**

1. **Each instruction = New layer**
2. **Layers are cached** (speeds up builds)
3. **Layers are shared** between images
4. **Read-only** once created
5. **Container = Image + Writable layer**

#### 📝 Example: How Layers Work

```dockerfile
FROM ubuntu:22.04          # Layer 1 (Base OS)
RUN apt-get update         # Layer 2 (Update packages)
RUN apt-get install -y nginx  # Layer 3 (Install nginx)
COPY index.html /var/www/html/  # Layer 4 (Copy file)
CMD ["nginx", "-g", "daemon off;"]  # Layer 5 (Start command)
```

Each `RUN`, `COPY`, `ADD` creates a new layer.

#### 🔍 View Image Layers

```bash
# See layers of an image
docker history nginx:alpine

# Output shows:
# IMAGE          CREATED       CREATED BY                                      SIZE
# abc123         2 weeks ago   CMD ["nginx" "-g" "daemon off;"]               0B
# def456         2 weeks ago   COPY index.html /usr/share/nginx/html/         4kB
# ghi789         2 weeks ago   RUN apk add --no-cache nginx                   50MB
# ...
```

#### 🏪 Docker Hub & Registries

```bash
# Default registry: Docker Hub (hub.docker.com)

# Pull an image
docker pull nginx
docker pull nginx:1.25-alpine  # Specific version

# Pull from private registry
docker pull myregistry.com/myapp:v1.0

# Search for images
docker search nginx

# Official vs Community images
# Official: nginx, ubuntu, node (verified by Docker)
# Community: username/imagename
```

#### 🛠️ Image Operations

```bash
# List all images
docker images
docker image ls

# Pull image from registry
docker pull ubuntu:22.04

# Tag an image (create alias)
docker tag nginx:latest myapp:v1.0
docker tag myapp:v1.0 myregistry.com/myapp:v1.0

# Push image to registry
docker login  # Login first
docker push myregistry.com/myapp:v1.0

# Remove image
docker rmi nginx:latest
docker image rm nginx:latest

# Remove multiple images
docker rmi $(docker images -q)
```

#### 🔍 Image Inspection

```bash
# Detailed information about an image
docker inspect nginx:alpine

# See specific fields
docker inspect nginx:alpine --format='{{.Architecture}}'
docker inspect nginx:alpine --format='{{.Config.Env}}'

# Check image size
docker images nginx:alpine --format "{{.Size}}"

# See image layers in detail
docker history nginx:alpine --no-trunc
```

#### 🗑️ Dangling Images

**Simple Explanation:**
Dangling images are "orphaned" images that have no tag and are not used by any container.

```bash
# How dangling images are created:
docker build -t myapp:v1 .
docker build -t myapp:v1 .  # Rebuild with same tag
# The old image becomes dangling (tag moved to new image)

# List dangling images
docker images -f "dangling=true"

# Remove dangling images
docker image prune

# Remove all unused images
docker image prune -a
```

#### 📝 Image Naming Convention

```
[registry-url]/[namespace]/[repository]:[tag]

Examples:
nginx                          # Official image
nginx:1.25                     # Specific version
nginx:1.25-alpine             # Variant
docker.io/library/nginx:latest # Full format
myregistry.com/team/app:v1.0  # Private registry
```

#### ✅ Best Practices

1. **Always use specific tags** (not `latest`)
   ```dockerfile
   # Bad
   FROM node:latest
   
   # Good
   FROM node:18.17.1-alpine
   ```

2. **Use official images** when possible

3. **Keep images small** (prefer Alpine variants)

4. **Clean up regularly**
   ```bash
   docker image prune -a --filter "until=24h"
   ```

---

### 7. Docker Containers Deep Dive

#### 💡 Simple Explanation

If an image is a recipe, a container is the actual dish you cook. It's a **running instance** of an image.

#### 🔄 Container Lifecycle

```
        docker create
             ↓
        ┌─────────┐
        │ CREATED │
        └────┬────┘
             │ docker start
             ↓
        ┌─────────┐     docker pause
        │ RUNNING │ ←─────────────┐
        └────┬────┘                │
             │                     │
             │ docker pause   ┌────┴────┐
             └───────────────→│ PAUSED  │
             │                └─────────┘
             │ docker stop          ↑
             ↓                      │
        ┌─────────┐                 │
        │ STOPPED │─────────────────┘
        └────┬────┘     docker unpause
             │
             │ docker rm
             ↓
        ┌─────────┐
        │ REMOVED │
        └─────────┘
```

#### 🚀 Running Containers

**Foreground vs Background:**

```bash
# Foreground (attached) - blocks terminal
docker run nginx
# You see logs, Ctrl+C stops container

# Background (detached) - runs in background
docker run -d nginx
# Returns container ID, terminal is free

# Run and get interactive shell
docker run -it ubuntu bash
# -i = interactive (keep STDIN open)
# -t = tty (allocate pseudo-terminal)

# Run in background with name
docker run -d --name my-nginx nginx
```

#### 🏷️ Container Naming

```bash
# Docker auto-generates names if not specified
docker run -d nginx
# Creates name like "quirky_einstein"

# Better: specify name
docker run -d --name web-server nginx

# Name must be unique
docker run -d --name web-server nginx  # Error: name already in use

# Remove and recreate
docker rm -f web-server
docker run -d --name web-server nginx
```

#### 🔄 Restart Policies

```bash
# no: Don't restart (default)
docker run -d --restart=no nginx

# on-failure: Restart if exits with error
docker run -d --restart=on-failure nginx
docker run -d --restart=on-failure:5 nginx  # Max 5 retries

# always: Always restart (even after reboot)
docker run -d --restart=always nginx

# unless-stopped: Like always, but respect manual stop
docker run -d --restart=unless-stopped nginx

# Update restart policy of running container
docker update --restart=always my-container
```

**Real-World Example:**
```bash
# Production web server with auto-restart
docker run -d \
  --name production-nginx \
  --restart=unless-stopped \
  -p 80:80 \
  nginx:1.25-alpine
```

#### ⚙️ Resource Limits

```bash
# Limit memory
docker run -d --memory="512m" nginx
docker run -d --memory="512m" --memory-swap="1g" nginx

# Limit CPU
docker run -d --cpus="1.5" nginx  # 1.5 CPU cores
docker run -d --cpu-shares=512 nginx  # Relative weight

# Limit both
docker run -d \
  --name resource-limited-app \
  --memory="1g" \
  --cpus="2" \
  --memory-swap="2g" \
  my-app:latest

# Check resource usage
docker stats
docker stats my-container

# Real-time resource monitoring
docker stats --no-stream
```

#### 📋 Container Logs

```bash
# View logs
docker logs my-container

# Follow logs (like tail -f)
docker logs -f my-container

# Last N lines
docker logs --tail 100 my-container

# Logs with timestamps
docker logs -t my-container

# Logs since specific time
docker logs --since 2024-01-01 my-container
docker logs --since 10m my-container  # Last 10 minutes

# Combination
docker logs -f --tail 50 --since 5m my-container
```

#### 🔧 Exec vs Attach

**docker exec** - Run NEW command in running container:
```bash
# Execute command
docker exec my-container ls /app

# Get interactive shell
docker exec -it my-container bash
docker exec -it my-container sh  # For Alpine

# Run as specific user
docker exec -u root my-container whoami

# Execute in specific directory
docker exec -w /app my-container pwd
```

**docker attach** - Attach to RUNNING process (PID 1):
```bash
# Attach to main process
docker attach my-container
# You see output of main process
# Ctrl+C will STOP the container!

# Attach without stopping (use Ctrl+P then Ctrl+Q to detach)
docker attach --sig-proxy=false my-container
```

**When to use what:**
- **exec**: Debug, run commands, get shell (most common)
- **attach**: View main process output (rarely used)

#### 🛠️ Container Management

```bash
# List running containers
docker ps
docker container ls

# List all containers (including stopped)
docker ps -a
docker container ls -a

# Pause container (freeze processes)
docker pause my-container
docker unpause my-container

# Stop container (graceful shutdown, 10s timeout)
docker stop my-container
docker stop -t 30 my-container  # 30s timeout

# Kill container (force kill immediately)
docker kill my-container

# Restart container
docker restart my-container

# Remove container
docker rm my-container

# Remove running container (force)
docker rm -f my-container

# Remove all stopped containers
docker container prune

# Remove all containers (dangerous!)
docker rm -f $(docker ps -aq)
```

#### 🔍 Container Inspection

```bash
# Full details
docker inspect my-container

# Specific field
docker inspect my-container --format='{{.State.Status}}'
docker inspect my-container --format='{{.NetworkSettings.IPAddress}}'

# Container process information
docker top my-container

# Container resource stats
docker stats my-container

# Container port mappings
docker port my-container

# Container filesystem changes
docker diff my-container
```

#### 💼 Practical Examples

**Example 1: Web Server with Proper Configuration**
```bash
docker run -d \
  --name production-web \
  --restart=unless-stopped \
  --memory="1g" \
  --cpus="2" \
  -p 80:80 \
  -p 443:443 \
  -v /var/www/html:/usr/share/nginx/html:ro \
  -v /etc/nginx/conf.d:/etc/nginx/conf.d:ro \
  nginx:1.25-alpine
```

**Example 2: Database with Persistence**
```bash
docker run -d \
  --name postgres-db \
  --restart=unless-stopped \
  --memory="2g" \
  -e POSTGRES_PASSWORD=secretpass \
  -e POSTGRES_USER=admin \
  -e POSTGRES_DB=myapp \
  -v postgres-data:/var/lib/postgresql/data \
  -p 5432:5432 \
  postgres:15-alpine
```

**Example 3: Development Environment**
```bash
docker run -it --rm \
  --name dev-env \
  -v $(pwd):/workspace \
  -w /workspace \
  -p 3000:3000 \
  node:18-alpine \
  sh
```

---

### 8. Dockerfile Mastery (Very Important)

#### 💡 Simple Explanation

A Dockerfile is a recipe for building Docker images. It's a text file with instructions telling Docker how to build your image.

#### 🎓 Professional Depth

**Dockerfile Structure:**

```dockerfile
# Comments start with #
# Instructions are UPPERCASE (convention)
# Each instruction creates a layer

# Syntax:
INSTRUCTION arguments
```

#### 🔧 Core Instructions

---

#### 1️⃣ FROM - Base Image

```dockerfile
# Always first instruction (except ARG)
FROM ubuntu:22.04

# Multi-platform
FROM --platform=linux/amd64 ubuntu:22.04

# From scratch (empty image)
FROM scratch

# Multiple FROM (multi-stage builds)
FROM node:18 AS builder
FROM nginx:alpine AS runner
```

---

#### 2️⃣ RUN - Execute Commands

```dockerfile
# Shell form (runs in /bin/sh -c)
RUN apt-get update && apt-get install -y nginx

# Exec form (doesn't invoke shell)
RUN ["apt-get", "update"]

# Multiple commands (creates multiple layers - BAD)
RUN apt-get update
RUN apt-get install -y nginx
RUN apt-get clean

# Better: Chain commands (single layer)
RUN apt-get update && \
    apt-get install -y nginx && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Alpine example
RUN apk add --no-cache \
    nginx \
    curl \
    && rm -rf /var/cache/apk/*
```

---

#### 3️⃣ CMD - Default Command

```dockerfile
# Only one CMD per Dockerfile (last one wins)
# Can be overridden at runtime

# Shell form
CMD npm start

# Exec form (preferred)
CMD ["npm", "start"]

# With ENTRYPOINT
CMD ["--port", "3000"]
```

---

#### 4️⃣ ENTRYPOINT - Container Executable

```dockerfile
# Makes container run as executable
# Cannot be overridden easily (need --entrypoint flag)

# Exec form
ENTRYPOINT ["nginx", "-g", "daemon off;"]

# With CMD (CMD becomes default arguments)
ENTRYPOINT ["node"]
CMD ["server.js"]

# Override at runtime:
# docker run myimage app.js  # Runs: node app.js
```

**CMD vs ENTRYPOINT Deep Dive:**

```dockerfile
# Example 1: CMD only
FROM ubuntu
CMD ["echo", "Hello"]
# docker run myimage           → Hello
# docker run myimage echo Bye  → Bye (CMD replaced)

# Example 2: ENTRYPOINT only
FROM ubuntu
ENTRYPOINT ["echo"]
# docker run myimage           → (no output)
# docker run myimage Hello     → Hello

# Example 3: Both (BEST PRACTICE)
FROM ubuntu
ENTRYPOINT ["echo"]
CMD ["Hello World"]
# docker run myimage           → Hello World
# docker run myimage Goodbye   → Goodbye
```

---

#### 5️⃣ COPY vs ADD (Critical Difference)

**Simple Explanation:**
- **COPY**: Simple file copy (preferred)
- **ADD**: Copy + extra features (auto-extract tar, download URLs)

**COPY:**
```dockerfile
# Basic copy
COPY index.html /var/www/html/

# Copy with patterns
COPY *.js /app/

# Copy directory
COPY src/ /app/src/

# Multiple sources
COPY package*.json /app/

# Change ownership
COPY --chown=user:group src/ /app/

# From build stage (multi-stage)
COPY --from=builder /app/dist /usr/share/nginx/html/
```

**ADD:**
```dockerfile
# Same as COPY
ADD index.html /var/www/html/

# Auto-extract tar files (can be dangerous)
ADD archive.tar.gz /app/
# Automatically extracts to /app/

# Download from URL (NOT recommended - no checksum verification)
ADD https://example.com/file.tar.gz /tmp/
```

**When to Use What:**

✅ **Use COPY** (99% of the time):
- Copying local files/directories
- Predictable behavior
- Security best practice

❌ **Avoid ADD** unless:
- You specifically need tar extraction
- Even then, be explicit:
  ```dockerfile
  COPY archive.tar.gz /tmp/
  RUN tar -xzf /tmp/archive.tar.gz -C /app/ && rm /tmp/archive.tar.gz
  ```

**Why COPY is Better:**
1. **Explicit**: Does exactly what it says
2. **Predictable**: No magic behavior
3. **Secure**: Doesn't auto-download from internet
4. **Recommended**: Docker best practices

---

#### 6️⃣ ENV - Environment Variables

```dockerfile
# Set environment variable
ENV NODE_ENV=production

# Multiple variables
ENV NODE_ENV=production \
    PORT=3000 \
    LOG_LEVEL=info

# Used in subsequent instructions
ENV APP_HOME=/app
WORKDIR $APP_HOME

# Override at runtime:
# docker run -e NODE_ENV=development myimage
```

---

#### 7️⃣ ARG - Build Arguments

```dockerfile
# Available only during build time
ARG VERSION=1.0
ARG NODE_VERSION=18

# Use in FROM
ARG NODE_VERSION=18
FROM node:${NODE_VERSION}

# Use in RUN
ARG BUILD_DATE
RUN echo "Built on ${BUILD_DATE}"

# Provide at build time:
# docker build --build-arg NODE_VERSION=20 .

# ARG vs ENV:
# ARG: Build time only
# ENV: Build time + runtime
```

---

#### 8️⃣ WORKDIR - Working Directory

```dockerfile
# Set working directory (creates if not exists)
WORKDIR /app

# All subsequent commands run from here
COPY . .
RUN npm install

# Use variables
ENV APP_DIR=/application
WORKDIR $APP_DIR

# Multiple WORKDIR (relative paths)
WORKDIR /app
WORKDIR subdir  # Now at /app/subdir
```

---

#### 9️⃣ EXPOSE - Document Ports

```dockerfile
# Document which ports the container listens on
EXPOSE 80
EXPOSE 443
EXPOSE 8080/tcp
EXPOSE 8081/udp

# Multiple ports
EXPOSE 80 443 8080

# NOTE: EXPOSE doesn't publish ports!
# It's documentation only
# Still need: docker run -p 80:80 myimage
```

---

#### 🔟 USER - Switch User

```dockerfile
# Switch to user (security best practice)
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser

# Everything after runs as appuser
RUN whoami  # Outputs: appuser

# Switch back to root
USER root
RUN apt-get update
USER appuser

# With UID:GID
USER 1000:1000
```

---

#### 1️⃣1️⃣ VOLUME - Declare Volumes

```dockerfile
# Declare volumes (creates mount point)
VOLUME /data

# Multiple volumes
VOLUME /data /logs

# NOTE: Better to define volumes at runtime
# docker run -v mydata:/data myimage
```

---

#### 1️⃣2️⃣ LABEL - Metadata

```dockerfile
# Add metadata to image
LABEL maintainer="your.email@example.com"
LABEL version="1.0"
LABEL description="My awesome application"

# Multiple labels
LABEL maintainer="admin@example.com" \
      version="2.0" \
      environment="production"
```

---

## 🎯 Quick Command Reference

### Image Commands
```bash
docker images                    # List all images
docker pull <image>              # Download image
docker build -t <name> .         # Build image from Dockerfile
docker tag <image> <new-tag>     # Tag an image
docker push <image>              # Push to registry
docker rmi <image>               # Remove image
docker history <image>           # View image layers
docker inspect <image>           # Detailed image info
docker image prune               # Remove dangling images
```

### Container Commands
```bash
docker run <image>               # Create and start container
docker run -d <image>            # Run in background (detached)
docker run -it <image> bash      # Run with interactive terminal
docker run --name <name> <image> # Run with custom name
docker ps                        # List running containers
docker ps -a                     # List all containers
docker stop <container>          # Stop container
docker start <container>         # Start stopped container
docker restart <container>       # Restart container
docker rm <container>            # Remove container
docker rm -f <container>         # Force remove running container
docker exec -it <container> bash # Execute command in container
docker logs <container>          # View container logs
docker logs -f <container>       # Follow logs
docker inspect <container>       # Detailed container info
docker stats                     # Resource usage statistics
docker top <container>           # Running processes
docker container prune           # Remove stopped containers
```

### Build Commands
```bash
docker build -t myapp:v1 .                    # Build with tag
docker build --no-cache -t myapp:v1 .        # Build without cache
docker build --build-arg VERSION=2.0 .       # Build with arguments
docker build -f Dockerfile.prod -t myapp .   # Specify Dockerfile
```

### System Commands
```bash
docker info                      # Docker system info
docker version                   # Docker version
docker system df                 # Disk usage
docker system prune              # Remove unused data
docker system prune -a           # Remove all unused data
docker system prune --volumes    # Include volumes
```

---

## 📚 Learning Tips & Best Practices

### Study Strategy
1. **Practice Daily**: Run commands hands-on
2. **Build Projects**: Best way to learn
3. **Read Error Messages**: They're helpful!
4. **Use Official Docs**: https://docs.docker.com
5. **Join Communities**: Forums, Stack Overflow, Reddit

### Dockerfile Best Practices
- Use specific base image tags (not `latest`)
- Minimize layers by chaining commands
- Order instructions from least to most frequently changing
- Use `.dockerignore` to exclude files
- Use multi-stage builds for smaller images
- Run as non-root user
- Keep images small (prefer Alpine)
- Use COPY instead of ADD
- Don't install unnecessary packages
- Clean up in the same layer

### Security Best Practices
- Never run containers as root in production
- Use official images from trusted sources
- Scan images for vulnerabilities
- Don't store secrets in images
- Use secrets management (Docker secrets, env vars)
- Limit container resources
- Use read-only filesystems when possible
- Keep base images updated

### Performance Best Practices
- Use layer caching effectively
- Minimize image size
- Use multi-stage builds
- Don't run multiple processes in one container
- Use volumes for persistent data
- Set resource limits appropriately
- Monitor container metrics

---

## 🔖 Quick Topic Finder

**Need to find something fast? Use Ctrl+F (or Cmd+F) and search for:**

### Concepts
- "containerization" - What Docker does
- "layers" - How images work
- "lifecycle" - Container states
- "registry" - Where images are stored

### Commands
- "docker run" - Start containers
- "docker build" - Build images
- "docker exec" - Run commands in container
- "docker logs" - View output
- "docker ps" - List containers
- "docker images" - List images

### Instructions
- "FROM" - Base image
- "RUN" - Execute commands
- "CMD" - Default command
- "COPY" - Copy files
- "ENV" - Environment variables
- "USER" - Switch user
- "WORKDIR" - Set directory

### Topics
- "installation" - How to install
- "security" - Best practices
- "non-root" - User management
- "restart policy" - Auto-restart
- "resource limits" - CPU/Memory
- "multi-stage" - Build optimization

---

## 📖 Next Learning Path

**You've completed Phase 1 & 2! Next up:**

### Phase 3: Advanced Concepts (Week 5-6)
- Docker Networking
- Docker Volumes & Data Management
- Docker Compose
- Multi-stage Builds Advanced
- Docker Registry Management

### Phase 4: Production & DevOps (Week 7-8)
- Container Orchestration (Kubernetes basics)
- CI/CD with Docker
- Docker Security in Depth
- Monitoring & Logging
- Production Deployment Strategies
- Troubleshooting

---

## 💡 Common Issues & Solutions

### Issue: Permission Denied
```bash
# Problem: docker: Got permission denied
# Solution: Add user to docker group
sudo usermod -aG docker $USER
# Then log out and log back in
```

### Issue: Port Already in Use
```bash
# Problem: Port is already allocated
# Solution: Check what's using the port
sudo lsof -i :80
# Or use a different port
docker run -p 8080:80 nginx
```

### Issue: Container Exits Immediately
```bash
# Problem: Container starts then stops
# Solution: Check logs
docker logs <container-name>
# Common cause: No foreground process
```

### Issue: Cannot Remove Image
```bash
# Problem: Image is referenced by container
# Solution: Remove container first
docker rm -f $(docker ps -aq)
# Then remove image
docker rmi <image-name>
```

---
# 🎯 50 Real-World Docker Interview Questions

> **Comprehensive collection of scenario-based Docker interview questions asked by top companies**

---

## 📋 Table of Contents
- [Beginner Level (1-15)](#beginner-level-questions-1-15)
- [Intermediate Level (16-35)](#intermediate-level-questions-16-35)
- [Advanced Level (36-50)](#advanced-level-questions-36-50)

---

## Beginner Level Questions (1-15)

### 1. Your application works on your laptop but fails in production. How does Docker solve this problem?

**Scenario:** You developed a Node.js application on your Windows laptop. It works perfectly. But when the DevOps team deploys it on a Linux server, it crashes with "module not found" errors.

**Answer:** 
Docker packages the application with all its dependencies (Node.js runtime, libraries, OS-level dependencies) into a container. This container runs identically on any environment - laptop, staging, or production. The container includes:
- Exact Node.js version
- All npm packages
- OS libraries
- Environment configuration

This eliminates the "it works on my machine" problem.

---

### 2. A container stopped unexpectedly in production. How do you troubleshoot it?

**Scenario:** Your production API container stopped at 3 AM. Users are complaining. What's your first step?

**Answer:**
```bash
# Step 1: Check if container is running
docker ps -a

# Step 2: Check the logs to see why it stopped
docker logs <container-name>

# Step 3: Check the exit code
docker inspect <container-name> --format='{{.State.ExitCode}}'
# Exit code 0 = normal, 1 = error, 137 = killed by SIGKILL

# Step 4: Try to restart
docker start <container-name>

# Step 5: If persistent issue, check resource usage
docker stats
```

Common causes: Out of memory, application crash, dependency failure, health check failure.

---

### 3. How do you limit a container to use only 512MB RAM and 1 CPU core?

**Scenario:** Your Java application container is consuming too much memory and affecting other services on the same host.

**Answer:**
```bash
docker run -d \
  --name my-java-app \
  --memory="512m" \
  --memory-swap="512m" \
  --cpus="1.0" \
  my-java-app:latest
```

To update running container:
```bash
docker update --memory="512m" --cpus="1.0" my-java-app
```

Monitor:
```bash
docker stats my-java-app
```

---

### 4. Your Docker image is 2GB in size. How do you reduce it?

**Scenario:** Building and deploying takes too long because your Python application image is huge.

**Answer:**

**Before (Bad):**
```dockerfile
FROM ubuntu:22.04
RUN apt-get update
RUN apt-get install -y python3 python3-pip
COPY requirements.txt .
RUN pip3 install -r requirements.txt
COPY . /app
```

**After (Good):**
```dockerfile
# Use Alpine (smaller base)
FROM python:3.11-alpine

# Install dependencies in one layer
RUN apk add --no-cache gcc musl-dev

WORKDIR /app

# Copy only requirements first (layer caching)
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY . .

# Remove unnecessary files
RUN rm -rf /var/cache/apk/*

CMD ["python", "app.py"]
```

Additional tips:
- Use `.dockerignore` file
- Multi-stage builds
- Don't install dev dependencies in production

---

### 5. Container data is lost when you restart it. How do you persist data?

**Scenario:** Your MySQL container stores data. When you restart it, all data is gone.

**Answer:**
```bash
# Create a named volume
docker volume create mysql-data

# Run container with volume
docker run -d \
  --name mysql-db \
  -e MYSQL_ROOT_PASSWORD=secret \
  -v mysql-data:/var/lib/mysql \
  mysql:8.0

# Even after removing container, data persists
docker rm -f mysql-db

# Start new container with same volume
docker run -d \
  --name mysql-db-new \
  -e MYSQL_ROOT_PASSWORD=secret \
  -v mysql-data:/var/lib/mysql \
  mysql:8.0
# All data is still there!
```

---

### 6. How do you run a container that automatically restarts if it crashes?

**Scenario:** Your monitoring service container occasionally crashes due to memory spikes. You want it to restart automatically.

**Answer:**
```bash
docker run -d \
  --name monitoring-service \
  --restart=unless-stopped \
  monitoring:latest

# Options:
# --restart=no              # Don't restart (default)
# --restart=on-failure      # Restart only if error
# --restart=on-failure:5    # Max 5 restart attempts
# --restart=always          # Always restart (even after reboot)
# --restart=unless-stopped  # Restart unless manually stopped
```

Update existing container:
```bash
docker update --restart=unless-stopped monitoring-service
```

---

### 7. You need to access a shell inside a running container. How?

**Scenario:** Your Node.js application is behaving strangely. You need to check files and run commands inside the container.

**Answer:**
```bash
# For containers with bash
docker exec -it my-nodejs-app bash

# For Alpine containers (no bash)
docker exec -it my-nodejs-app sh

# Run specific command
docker exec my-nodejs-app ls -la /app

# Run as root user (for debugging)
docker exec -u root -it my-nodejs-app bash

# Check environment variables
docker exec my-nodejs-app env
```

---

### 8. How do you copy files from your host to a running container?

**Scenario:** You need to update a configuration file in a running production container without restarting it.

**Answer:**
```bash
# Copy file TO container
docker cp config.json my-container:/app/config.json

# Copy file FROM container
docker cp my-container:/app/logs/error.log ./local-error.log

# Copy entire directory
docker cp ./configs my-container:/etc/app/
```

**Note:** This is for emergency fixes. Proper way is to rebuild the image.

---

### 9. Your application needs to connect to a database. How do you pass the database password securely?

**Scenario:** Your app needs credentials. Hardcoding in Dockerfile is insecure.

**Answer:**
```bash
# Method 1: Environment variables (simple)
docker run -d \
  --name my-app \
  -e DB_HOST=mysql \
  -e DB_USER=admin \
  -e DB_PASSWORD=secret123 \
  my-app:latest

# Method 2: Environment file
# Create .env file:
# DB_HOST=mysql
# DB_USER=admin
# DB_PASSWORD=secret123

docker run -d \
  --name my-app \
  --env-file .env \
  my-app:latest

# Method 3: Docker secrets (Swarm mode - most secure)
echo "secret123" | docker secret create db_password -

docker service create \
  --name my-app \
  --secret db_password \
  my-app:latest
```

**Never** put passwords in Dockerfile!

---

### 10. How do you view real-time logs from a running container?

**Scenario:** Your API is throwing errors and you need to monitor logs in real-time.

**Answer:**
```bash
# Follow logs (like tail -f)
docker logs -f my-api

# Last 100 lines + follow
docker logs -f --tail 100 my-api

# Show timestamps
docker logs -f -t my-api

# Logs from last 10 minutes
docker logs --since 10m my-api

# Logs from specific time
docker logs --since 2024-01-11T10:00:00 my-api
```

---

### 11. Multiple containers need to communicate. How do you set this up?

**Scenario:** Your web app (container 1) needs to connect to Redis (container 2) and PostgreSQL (container 3).

**Answer:**
```bash
# Create custom network
docker network create my-app-network

# Run database
docker run -d \
  --name postgres-db \
  --network my-app-network \
  -e POSTGRES_PASSWORD=secret \
  postgres:15

# Run Redis
docker run -d \
  --name redis-cache \
  --network my-app-network \
  redis:7-alpine

# Run application
docker run -d \
  --name web-app \
  --network my-app-network \
  -p 8080:8080 \
  my-web-app:latest

# Inside web-app container, connect to:
# - postgres-db:5432
# - redis-cache:6379
```

Containers can reach each other by **container name** as hostname.

---

### 12. How do you remove all stopped containers to free up space?

**Scenario:** Your server has 50+ stopped containers consuming disk space.

**Answer:**
```bash
# Remove all stopped containers
docker container prune

# With confirmation
docker container prune -f

# Remove containers stopped for more than 24 hours
docker container prune --filter "until=24h"

# Nuclear option: Remove ALL containers (running + stopped)
docker rm -f $(docker ps -aq)

# Check disk space
docker system df
```

---

### 13. You built an image but forgot to tag it. How do you tag it now?

**Scenario:** You ran `docker build .` and got an image with ID abc123. You need to tag it.

**Answer:**
```bash
# Tag by image ID
docker tag abc123 my-app:v1.0

# Tag with registry
docker tag abc123 myregistry.com/my-app:v1.0

# Create multiple tags
docker tag abc123 my-app:v1.0
docker tag abc123 my-app:latest
docker tag abc123 my-app:production

# View all tags
docker images my-app
```

---

### 14. How do you expose a container's port to the host machine?

**Scenario:** Your nginx container runs on port 80 inside container. You want to access it on port 8080 from your browser.

**Answer:**
```bash
# Map port 8080 (host) to 80 (container)
docker run -d -p 8080:80 nginx

# Map to all interfaces
docker run -d -p 0.0.0.0:8080:80 nginx

# Map to specific interface
docker run -d -p 127.0.0.1:8080:80 nginx

# Random port on host
docker run -d -P nginx  # Docker assigns random port

# Multiple ports
docker run -d \
  -p 8080:80 \
  -p 8443:443 \
  nginx

# Check which ports are mapped
docker port <container-name>
```

---

### 15. How do you check which version of Docker is installed?

**Scenario:** Before running commands, you need to verify Docker version for compatibility.

**Answer:**
```bash
# Short version
docker --version
# Output: Docker version 24.0.6

# Detailed version info
docker version

# System-wide info
docker info
```

---

## Intermediate Level Questions (16-35)

### 16. Your application needs different configurations for dev, staging, and production. How do you handle this with Docker?

**Scenario:** Same application, different database URLs, API keys, and debug settings per environment.

**Answer:**

**Dockerfile:**
```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
EXPOSE 3000
CMD ["node", "server.js"]
```

**Run with environment-specific configs:**
```bash
# Development
docker run -d \
  --name app-dev \
  -e NODE_ENV=development \
  -e DB_URL=postgres://dev-db:5432/myapp \
  -e DEBUG=true \
  -p 3000:3000 \
  my-app:latest

# Staging
docker run -d \
  --name app-staging \
  -e NODE_ENV=staging \
  -e DB_URL=postgres://staging-db:5432/myapp \
  -e DEBUG=false \
  -p 3001:3000 \
  my-app:latest

# Production
docker run -d \
  --name app-prod \
  -e NODE_ENV=production \
  -e DB_URL=postgres://prod-db:5432/myapp \
  -e DEBUG=false \
  --restart=unless-stopped \
  -p 80:3000 \
  my-app:latest
```

Or use config files:
```bash
docker run -d --env-file .env.production my-app:latest
```

---

### 17. A container is using 100% CPU and slowing down the host. How do you identify and fix it?

**Scenario:** Server is slow. Multiple containers are running. Need to find the culprit.

**Answer:**
```bash
# Step 1: Check all containers' resource usage
docker stats

# Step 2: Identify the problematic container (100% CPU)
# Let's say it's "api-service"

# Step 3: Check what's running inside
docker top api-service

# Step 4: Limit CPU usage
docker update --cpus="1.0" api-service

# Step 5: Check logs for issues
docker logs --tail 100 api-service

# Step 6: If it's a code issue, restart with limits
docker stop api-service
docker run -d \
  --name api-service \
  --cpus="1.5" \
  --memory="1g" \
  api-service:latest

# Monitor again
docker stats api-service
```

---

### 18. How do you create a Dockerfile for a multi-stage build to reduce image size?

**Scenario:** Your React app with Node.js build tools creates a 1.5GB image. You only need the built files.

**Answer:**
```dockerfile
# Stage 1: Build stage
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build
# At this point, /app/build has production files

# Stage 2: Production stage
FROM nginx:alpine
# Copy only built files from builder stage
COPY --from=builder /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

**Result:** 
- Builder stage: 1.5GB (not in final image)
- Final image: 25MB (only nginx + built files)

**Another example (Go application):**
```dockerfile
# Build stage
FROM golang:1.21-alpine AS builder
WORKDIR /app
COPY . .
RUN go build -o main .

# Production stage
FROM alpine:latest
COPY --from=builder /app/main /main
CMD ["/main"]
```

---

### 19. How do you debug a container that exits immediately after starting?

**Scenario:** You run `docker run my-app` and it exits instantly. `docker logs` shows nothing.

**Answer:**
```bash
# Step 1: Check exit code
docker inspect <container-name> --format='{{.State.ExitCode}}'

# Step 2: Try running with shell override
docker run -it --entrypoint sh my-app

# Step 3: Check if CMD/ENTRYPOINT is correct
docker inspect my-app --format='{{.Config.Cmd}}'
docker inspect my-app --format='{{.Config.Entrypoint}}'

# Step 4: Run in foreground to see errors
docker run --rm my-app

# Step 5: Keep container alive for debugging
docker run -d --entrypoint tail my-app -f /dev/null
docker exec -it <container> sh
```

**Common causes:**
- No foreground process (container needs a process that doesn't exit)
- Wrong CMD/ENTRYPOINT
- Application crash on startup
- Missing dependencies

---

### 20. How do you update a running container without downtime?

**Scenario:** You have a production web service. New version is ready. Need zero downtime deployment.

**Answer:**

**Strategy: Blue-Green Deployment**
```bash
# Current version (blue) running on port 80
docker run -d --name web-blue -p 80:8080 my-app:v1.0

# Start new version (green) on different port
docker run -d --name web-green -p 8080:8080 my-app:v2.0

# Test new version
curl http://localhost:8080/health

# Switch traffic (update load balancer or nginx)
# If using nginx, update upstream, reload nginx

# Once verified, stop old version
docker stop web-blue
docker rm web-blue

# Rename new version
docker rename web-green web-blue
```

**Better approach: Use Docker Compose or Kubernetes for rolling updates**

---

### 21. Your Dockerfile uses COPY but some files shouldn't be included. How do you exclude them?

**Scenario:** Your project has `node_modules`, `.git`, test files that shouldn't be in the image.

**Answer:**

**Create `.dockerignore` file:**
```
# .dockerignore
node_modules
npm-debug.log
.git
.gitignore
README.md
.env
.env.local
*.test.js
coverage/
.vscode/
.idea/
*.log
dist/
build/
```

**Dockerfile:**
```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .  # Only copies files NOT in .dockerignore
CMD ["node", "server.js"]
```

**Benefits:**
- Smaller image size
- Faster builds
- No sensitive files in image
- No unnecessary files

---

### 22. How do you run multiple containers with a single command?

**Scenario:** Your app needs web server, database, and cache. You want to start all together.

**Answer:**

**Create `docker-compose.yml`:**
```yaml
version: '3.8'

services:
  web:
    image: nginx:alpine
    ports:
      - "80:80"
    depends_on:
      - api
    networks:
      - app-network

  api:
    build: .
    environment:
      DB_HOST: postgres
      REDIS_HOST: redis
    depends_on:
      - postgres
      - redis
    networks:
      - app-network

  postgres:
    image: postgres:15-alpine
    environment:
      POSTGRES_PASSWORD: secret
    volumes:
      - db-data:/var/lib/postgresql/data
    networks:
      - app-network

  redis:
    image: redis:7-alpine
    networks:
      - app-network

networks:
  app-network:
    driver: bridge

volumes:
  db-data:
```

**Commands:**
```bash
# Start all services
docker-compose up -d

# View status
docker-compose ps

# View logs
docker-compose logs -f

# Stop all
docker-compose down

# Stop and remove volumes
docker-compose down -v
```

---

### 23. How do you secure a container by running it as a non-root user?

**Scenario:** Security team requires all containers to run as non-root users.

**Answer:**
```dockerfile
FROM node:18-alpine

# Create non-root user
RUN addgroup -g 1001 -S nodejs && \
    adduser -S nodejs -u 1001 -G nodejs

# Create app directory with correct permissions
WORKDIR /app
RUN chown -R nodejs:nodejs /app

# Copy files as root
COPY package*.json ./
RUN npm ci --only=production

COPY . .

# Switch to non-root user
USER nodejs

# Now everything runs as nodejs user
EXPOSE 3000
CMD ["node", "server.js"]
```

**Verify:**
```bash
docker exec <container> whoami
# Output: nodejs (not root)

docker exec <container> id
# Output: uid=1001(nodejs) gid=1001(nodejs)
```

---

### 24. Container logs are filling up disk space. How do you limit log size?

**Scenario:** Docker logs have consumed 50GB of disk space.

**Answer:**

**Method 1: Configure daemon globally**

Edit `/etc/docker/daemon.json`:
```json
{
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "10m",
    "max-file": "3"
  }
}
```

Restart Docker:
```bash
sudo systemctl restart docker
```

**Method 2: Per container**
```bash
docker run -d \
  --name my-app \
  --log-opt max-size=10m \
  --log-opt max-file=3 \
  my-app:latest
```

**Method 3: Use different log driver**
```bash
docker run -d \
  --name my-app \
  --log-driver=syslog \
  my-app:latest
```

**Clean existing logs:**
```bash
# Truncate logs of running container
truncate -s 0 $(docker inspect --format='{{.LogPath}}' <container>)

# Or use script
echo "" > $(docker inspect --format='{{.LogPath}}' <container>)
```

---

### 25. How do you share data between multiple containers?

**Scenario:** Container A generates reports, Container B serves them via web interface.

**Answer:**
```bash
# Create shared volume
docker volume create shared-data

# Container A: Generates reports
docker run -d \
  --name report-generator \
  -v shared-data:/reports \
  report-generator:latest

# Container B: Serves reports
docker run -d \
  --name report-viewer \
  -v shared-data:/usr/share/nginx/html:ro \
  -p 80:80 \
  nginx:alpine

# Both containers access same data
# Container A writes to /reports
# Container B reads from /usr/share/nginx/html
```

**Alternative: Mount same host directory:**
```bash
mkdir -p /opt/shared-reports

docker run -d \
  --name report-generator \
  -v /opt/shared-reports:/reports \
  report-generator:latest

docker run -d \
  --name report-viewer \
  -v /opt/shared-reports:/usr/share/nginx/html:ro \
  -p 80:80 \
  nginx:alpine
```

---

### 26. How do you monitor container health and automatically restart unhealthy containers?

**Scenario:** Your API sometimes hangs. You want Docker to detect and restart it automatically.

**Answer:**

**In Dockerfile:**
```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY . .
RUN npm ci --only=production

# Health check
HEALTHCHECK --interval=30s --timeout=3s --start-period=40s --retries=3 \
  CMD node healthcheck.js || exit 1

CMD ["node", "server.js"]
```

**healthcheck.js:**
```javascript
const http = require('http');
const options = {
  host: 'localhost',
  port: 3000,
  path: '/health',
  timeout: 2000
};

http.get(options, (res) => {
  if (res.statusCode === 200) {
    process.exit(0);
  } else {
    process.exit(1);
  }
}).on('error', () => {
  process.exit(1);
});
```

**Run with restart policy:**
```bash
docker run -d \
  --name api-service \
  --restart=on-failure:3 \
  api-service:latest
```

**Check health status:**
```bash
docker ps  # Shows (healthy) or (unhealthy)
docker inspect api-service --format='{{.State.Health.Status}}'
```

---

### 27. How do you pass build-time variables to Docker build?

**Scenario:** You want to build images for different environments with different versions.

**Answer:**
```dockerfile
# Dockerfile
ARG NODE_VERSION=18
ARG BUILD_DATE
ARG VERSION

FROM node:${NODE_VERSION}-alpine

LABEL build_date=${BUILD_DATE}
LABEL version=${VERSION}

WORKDIR /app
COPY . .

RUN echo "Building version ${VERSION} on ${BUILD_DATE}"

CMD ["node", "server.js"]
```

**Build with arguments:**
```bash
# Default values
docker build -t my-app:latest .

# Custom values
docker build \
  --build-arg NODE_VERSION=20 \
  --build-arg BUILD_DATE=$(date -u +'%Y-%m-%dT%H:%M:%SZ') \
  --build-arg VERSION=2.0.1 \
  -t my-app:2.0.1 .
```

**View build args in image:**
```bash
docker inspect my-app:2.0.1 --format='{{.Config.Labels}}'
```

---

### 28. Your container needs to access the host's network services. How?

**Scenario:** Container needs to connect to a database running on the host machine (localhost).

**Answer:**

**Method 1: Host network mode**
```bash
docker run -d \
  --name my-app \
  --network host \
  my-app:latest

# Container can access host's localhost directly
# No port mapping needed
```

**Method 2: Special DNS name (Mac/Windows Docker Desktop)**
```bash
docker run -d \
  --name my-app \
  -e DB_HOST=host.docker.internal \
  my-app:latest

# Inside container, connect to: host.docker.internal:5432
```

**Method 3: Host IP (Linux)**
```bash
# Find host IP on docker bridge
ip addr show docker0

docker run -d \
  --name my-app \
  -e DB_HOST=172.17.0.1 \
  my-app:latest
```

---

### 29. How do you backup and restore Docker volumes?

**Scenario:** You need to backup production database volume before upgrade.

**Answer:**

**Backup volume:**
```bash
# Create backup directory
mkdir -p /backup

# Backup volume to tar file
docker run --rm \
  -v postgres-data:/data \
  -v /backup:/backup \
  alpine \
  tar czf /backup/postgres-backup-$(date +%Y%m%d).tar.gz -C /data .

# Or using existing container
docker run --rm \
  --volumes-from postgres-db \
  -v /backup:/backup \
  alpine \
  tar czf /backup/postgres-backup.tar.gz -C /var/lib/postgresql/data .
```

**Restore volume:**
```bash
# Create new volume
docker volume create postgres-data-restored

# Restore from backup
docker run --rm \
  -v postgres-data-restored:/data \
  -v /backup:/backup \
  alpine \
  tar xzf /backup/postgres-backup-20240111.tar.gz -C /data

# Use restored volume
docker run -d \
  --name postgres-restored \
  -v postgres-data-restored:/var/lib/postgresql/data \
  postgres:15
```

---

### 30. How do you find and remove unused Docker resources (images, containers, volumes)?

**Scenario:** Server disk is 95% full. Need to clean up Docker resources.

**Answer:**
```bash
# Check disk usage
docker system df
docker system df -v  # Detailed

# Remove stopped containers
docker container prune

# Remove unused images
docker image prune  # Dangling images only
docker image prune -a  # All unused images

# Remove unused volumes
docker volume prune

# Remove unused networks
docker network prune

# Remove everything unused (CAREFUL!)
docker system prune

# Aggressive cleanup (removes all unused resources)
docker system prune -a --volumes

# With time filter (remove resources older than 24h)
docker system prune --filter "until=24h"

# Check space saved
docker system df
```

---

### 31. How do you inspect network configuration of a running container?

**Scenario:** Container can't connect to another service. Need to debug networking.

**Answer:**
```bash
# View all networks
docker network ls

# Inspect specific network
docker network inspect bridge

# View container's network config
docker inspect my-container --format='{{.NetworkSettings.Networks}}'

# Get IP address
docker inspect my-container --format='{{.NetworkSettings.IPAddress}}'

# Get all network details
docker inspect my-container | jq '.[0].NetworkSettings'

# Test connectivity from container
docker exec my-container ping other-container
docker exec my-container curl http://other-container:8080

# Check DNS resolution
docker exec my-container nslookup other-container

# View port mappings
docker port my-container
```

---

### 32. How do you build an image without using cache?

**Scenario:** Previous build had errors. You want a completely fresh build.

**Answer:**
```bash
# Build without cache
docker build --no-cache -t my-app:latest .

# Pull latest base image and build without cache
docker build --pull --no-cache -t my-app:latest .

# Remove specific image and rebuild
docker rmi my-app:latest
docker build -t my-app:latest .
```

**When to use:**
- Debugging build issues
- Base image was updated
- Want fresh package installations
- Previous build had errors

---

### 33. Container needs to run a task at startup before the main application. How?

**Scenario:** Database needs migrations before starting, or need to wait for another service.

**Answer:**

**Method 1: Custom entrypoint script**

**entrypoint.sh:**
```bash
#!/bin/sh
set -e

# Wait for database
echo "Waiting for database..."
while ! nc -z postgres 5432; do
  sleep 1
done
echo "Database is ready!"

# Run migrations
echo "Running migrations..."
npm run migrate

# Start main application
echo "Starting application..."
exec "$@"
```

**Dockerfile:**
```dockerfile
FROM node:18-alpine

WORKDIR /app

# Install netcat for waiting
RUN apk add --no-cache netcat-openbsd

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

COPY . .
RUN npm ci --only=production

ENTRYPOINT ["/entrypoint.sh"]
CMD ["node", "server.js"]
```

**Method 2: Using init container pattern (Docker Compose)**
```yaml
version: '3.8'
services:
  init:
    image: my-app:latest
    command: npm run migrate
    depends_on:
      - postgres
  
  app:
    image: my-app:latest
    depends_on:
      init:
        condition: service_completed_successfully
```

---

### 34. How do you copy running container to create a new image?

**Scenario:** You made manual changes in a container for testing. Want to save them as a new image.

**Answer:**
```bash
# Make changes in running container
docker exec -it my-container bash
# ... make changes ...
# exit

# Commit changes to new image
docker commit my-container my-new-image:v1.0

# With metadata
docker commit \
  --author "John Doe <john@example.com>" \
  --message "Added custom configuration" \
  my-container \
  my-new-image:v1.0

# Verify new image
docker images my-new-image

# Run new image
docker run -d my-new-image:v1.0
```

**Note:** This is for testing only. For production, update Dockerfile and rebuild properly.

---

### 35. How do you limit network bandwidth for a container?

**Scenario:** A container is consuming too much network bandwidth, affecting other services.

**Answer:**
```bash
# Linux only - requires tc (traffic control)

# Create container
docker run -d --name bandwidth-limited my-app

# Limit to 1 Mbps
docker exec bandwidth-limited tc qdisc add dev eth0 root tbf rate 1mbit burst 32kbit latency 400ms

# Or use docker run with network settings (if supported)
docker run -d \
  --name bandwidth-limited \
  --network custom-network \
  --network-alias my-
---

## 🎓 Certification & Career Path

### Certifications
- Docker Certified Associate (DCA)
- Kubernetes certifications (CKA, CKAD)
- AWS/Azure/GCP container certifications

### Job Roles
- DevOps Engineer
- Container Platform Engineer
- Site Reliability Engineer (SRE)
- Cloud Engineer
- Software Engineer (with containerization skills)

---

**Last Updated:** January 2026  
**Version:** 1.0 Complete  
**Status:** Phase 1 & 2 Complete with all commands and examples

---

## 📞 Community Resources

- **Official Docs**: https://docs.docker.com
- **Docker Hub**: https://hub.docker.com
- **Docker Forums**: https://forums.docker.com
- **Stack Overflow**: Tag "docker"
- **Reddit**: r/docker
- **YouTube**: Docker official channel

---

*Happy Learning! 🐳*
