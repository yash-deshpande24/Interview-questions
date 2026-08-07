# Docker Commands — Types & Uses

Docker commands can be grouped into **8 main categories** based on what they manage: Images, Containers, Volumes, Networks, Docker Compose, System, Registry, and Build. Below is each category with the most important commands and their use.

---

## 1. Image Commands
Used to create, manage, and remove Docker images (the blueprint for containers).

| Command | Use |
|---|---|
| `docker build -t <name> .` | Build an image from a Dockerfile |
| `docker images` | List all images on your machine |
| `docker pull <image>` | Download an image from Docker Hub |
| `docker push <image>` | Upload an image to a registry |
| `docker rmi <image>` | Remove an image |
| `docker tag <image> <new-name>` | Rename/tag an image |
| `docker history <image>` | Show the layers/history of an image |

---

## 2. Container Commands
Used to create, run, stop, and manage containers (running instances of images).

| Command | Use |
|---|---|
| `docker run <image>` | Create and start a container from an image |
| `docker run -d <image>` | Run a container in the background (detached mode) |
| `docker run -p 8080:80 <image>` | Map a host port to a container port |
| `docker ps` | List running containers |
| `docker ps -a` | List all containers (running + stopped) |
| `docker stop <container>` | Stop a running container |
| `docker start <container>` | Start a stopped container |
| `docker restart <container>` | Restart a container |
| `docker rm <container>` | Remove a container |
| `docker exec -it <container> bash` | Open a shell inside a running container |
| `docker logs <container>` | View logs of a container |
| `docker inspect <container>` | Show detailed info (config, network, mounts) |
| `docker cp <container>:<path> <local-path>` | Copy files between container and host |

---

## 3. Volume Commands
Used to manage persistent data storage that survives even after a container is deleted.

| Command | Use |
|---|---|
| `docker volume create <name>` | Create a volume |
| `docker volume ls` | List all volumes |
| `docker volume inspect <name>` | Show volume details |
| `docker volume rm <name>` | Remove a volume |
| `docker run -v <volume>:<path> <image>` | Attach a volume to a container |

---

## 4. Network Commands
Used to manage how containers talk to each other and the outside world.

| Command | Use |
|---|---|
| `docker network ls` | List all networks |
| `docker network create <name>` | Create a custom network |
| `docker network inspect <name>` | Show network details |
| `docker network connect <network> <container>` | Connect a container to a network |
| `docker network rm <name>` | Remove a network |

---

## 5. Docker Compose Commands
Used to manage multi-container applications defined in a `docker-compose.yml` file (you used this in CloudTask Manager).

| Command | Use |
|---|---|
| `docker-compose up` | Start all services defined in compose file |
| `docker-compose up -d` | Start services in background |
| `docker-compose down` | Stop and remove all services |
| `docker-compose build` | Build images for services |
| `docker-compose logs` | View logs of all services |
| `docker-compose ps` | List running compose services |

---

## 6. System Commands
Used to check overall Docker status and clean up unused resources.

| Command | Use |
|---|---|
| `docker info` | Show system-wide Docker info |
| `docker version` | Show Docker version details |
| `docker system df` | Show disk space used by Docker |
| `docker system prune` | Remove all unused containers, images, and networks |
| `docker stats` | Show live resource usage (CPU, memory) of containers |

---

## 7. Registry Commands
Used to log in and manage images on Docker Hub or private registries (used with ECR in your AWS work).

| Command | Use |
|---|---|
| `docker login` | Log in to Docker Hub or a private registry |
| `docker logout` | Log out from a registry |
| `docker push <image>` | Upload image to registry |
| `docker pull <image>` | Download image from registry |

---

## 8. Build-related Commands
Used specifically during the image build process.

| Command | Use |
|---|---|
| `docker build -t <name>:<tag> .` | Build image with a tag |
| `docker build --no-cache .` | Build without using cache (fresh build) |
| `docker buildx build` | Build images for multiple platforms (e.g., ARM + x86) |

---

## Docker Volumes — Explained

**What is a Volume?**
A volume is a place to store data outside the container, so the data stays safe even if the container is deleted or restarted. Normally, when a container is removed, all its data is lost — volumes solve this problem.

**Types of Volumes:**

| Type | Description | Use Case |
|---|---|---|
| **Named Volume** | Created and managed by Docker (`docker volume create`) | Best for databases, persistent app data |
| **Bind Mount** | Links a folder on your host machine directly to the container | Best for local development (e.g., live code reload) |
| **tmpfs Mount** | Stores data only in memory (RAM), not on disk | Best for temporary, sensitive data (deleted on stop) |

**Simple Example:**
```
docker run -v mydata:/app/data myimage
```
This creates (or reuses) a volume called `mydata` and connects it to the `/app/data` folder inside the container.

**Interview Answer:**
"A Docker volume is used to store data outside the container so it doesn't get lost when the container stops or is removed. There are 3 types — named volumes, which Docker manages for you; bind mounts, which link a folder from your local machine to the container, useful during development; and tmpfs mounts, which store data only in memory for temporary use. In my CloudTask Manager project, I used volumes to persist PostgreSQL data even when containers were restarted."

---

## Docker Networking — Explained

**What is Docker Networking?**
Docker networking controls how containers communicate — with each other, with the host machine, and with the outside world.

**Types of Docker Networks:**

| Type | Description | Use Case |
|---|---|---|
| **Bridge (default)** | Creates a private internal network; containers on the same bridge can talk to each other | Default choice for most single-host apps |
| **Host** | Container shares the host machine's network directly (no isolation) | When you need maximum network performance, less common |
| **None** | Container has no network access at all | For fully isolated tasks (security-sensitive jobs) |
| **Overlay** | Connects containers across multiple Docker hosts/machines | Used in Docker Swarm / multi-host cluster setups |
| **Macvlan** | Gives a container its own MAC address, making it appear as a physical device on the network | Advanced/legacy app networking needs |

**Simple Example:**
```
docker network create mynetwork
docker run --network=mynetwork myimage
```
This creates a custom network and connects a container to it, so it can talk to other containers on the same network by name.

**Interview Answer:**
"Docker networking manages how containers communicate with each other and the outside world. The main types are bridge, which is the default and lets containers on the same host talk to each other; host, where the container shares the host's network directly; none, which blocks all networking; overlay, used for connecting containers across multiple machines in a cluster; and macvlan, for advanced setups. In my projects, I mainly used the default bridge network with Docker Compose, so my frontend, backend, and database containers could communicate with each other by service name."

---
**Q: How many types of Docker commands are there, and what are they used for?**

**A:** "Docker commands can be grouped into 8 main types — image commands, container commands, volume commands, network commands, Docker Compose commands, system commands, registry commands, and build commands. Image commands are used to build and manage images. Container commands are used to run, stop, and manage containers. Volume commands manage persistent storage. Network commands manage how containers connect with each other. Docker Compose commands let you run multi-container apps with one file — I used this in my CloudTask Manager project. System commands help clean up and monitor Docker. Registry commands are used to push and pull images from Docker Hub or private registries like AWS ECR."
