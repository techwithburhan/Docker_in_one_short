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
# docker run -e NODE_ENV=development
