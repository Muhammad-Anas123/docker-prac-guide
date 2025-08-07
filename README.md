# docker-prac-guide
A comprehensive collection of practical Docker CLI commands with detailed explanations, structured for revision, self-learning, and DevOps preparation. Ideal for beginners and intermediate learners who want to master Docker hands-on.
# 🐳 Docker Master Reference Guide
**By: Muhammad Anas**  
> A beginner-friendly, yet comprehensive documentation of Docker CLI commands and concepts, ideal for DevOps learners and revision.

---

## 📌 1. What Is Docker?

**Docker** is a platform that allows you to **build**, **package**, and **run applications in isolated environments** called containers. Unlike traditional virtual machines, containers are lightweight, fast, and portable because they share the host system's kernel.

### 📦 Why Use Docker?
- **Consistency**: Same app behavior in dev, staging, and prod.
- **Isolation**: Each app runs in its own container.
- **Portability**: Containers can run anywhere Docker is installed.
- **Efficiency**: Low resource usage compared to full VMs.

---

## ⚙️ 2. Docker Architecture Overview

```
Client  <-->  Docker Daemon  <-->  Docker Registry
   |                        |
   |                        +--> Containers (Running Apps)
   +--> Commands            +--> Images (App Blueprints)
```

- **Client**: Sends commands (`docker run`, `build`, etc.)
- **Docker Daemon**: Executes the commands
- **Registry**: Stores Docker images (e.g., Docker Hub, Amazon ECR)
- **Images**: Read-only templates used to create containers
- **Containers**: Live running instances created from images

---

## 🧰 3. Docker Setup and Installation

```bash
yum update -y
sudo yum install docker -y
which docker
docker -v
service docker start
service docker status
```

---

## ℹ️ 4. System Info & Container Overview

```bash
docker info
docker ps
docker ps -a
docker images
```

---

## 🚀 5. Running Your First Container

```bash
docker run -it ubuntu /bin/bash
docker run -it --name anascontainer ubuntu /bin/bash
```

---

## ⚙️ 6. Managing Docker Containers

```bash
docker start anascontainer
docker exec -it anascontainer bash
docker stop anascontainer
docker rm anascontainer
```

---

## 🔍 7. Inspecting and Debugging

```bash
docker diff anascontainer
history
```

---

## 📸 8. Saving & Reusing Container Work

```bash
docker commit anascontainer updateimage
docker images
```

---

## 🧪 9. Creating Containers from Custom Images

```bash
docker run -it --name practicecontainer updateimage /bin/bash
```

---

## 🛠️ 10. Building Docker Images via Dockerfile

### Dockerfile
```Dockerfile
FROM ubuntu:latest
RUN echo "I am learning DevOps" > /tmp/testfile
```

```bash
docker build -t testimage .
docker run -it --name testcontainer testimage /bin/bash
cat /tmp/testfile
```

---

## 📦 11. Docker Volumes: Data Persistence

### Share Data Between Containers
```bash
docker run -it --name container1 myimage /bin/bash
# Inside container1
mkdir myvolume && cd myvolume && touch file1 file2 file3

docker run -it --name container2 --volumes-from container1 ubuntu /bin/bash
cd myvolume && ls
```

### Map Host Directory
```bash
docker run -it --name hostcontainer -v /home/ec2-user:/vida ubuntu /bin/bash
cd /vida && ls
```

---

## 🧾 12. Adding Files to Image

### Dockerfile Example
```Dockerfile
FROM ubuntu:latest
COPY file1 /tmp/
COPY file2 /tmp/
RUN echo "My Docker Image with files" > /tmp/info.txt
```

```bash
docker build -t myimage:v2 .
docker run -it --name mycontainer2 myimage:v2 /bin/bash
ls /tmp && cat /tmp/info.txt
```

---

## 🧠 13. Summary: Most Useful Commands

| Command | Description |
|--------|-------------|
| `docker run -it image /bin/bash` | Create and run a container |
| `--name containername` | Give a name to container |
| `docker start` / `stop` / `rm` | Manage container lifecycle |
| `docker exec -it name bash` | Access a running container |
| `docker ps -a` | View all containers |
| `docker images` | List local images |
| `docker diff name` | See container file changes |
| `docker commit` | Save container as image |
| `docker build -t name .` | Build image from Dockerfile |
| `-v host:container` | Mount host volume |
| `--volumes-from name` | Share volume from container |
| `docker image/container prune` | Clean up unused resources |

---

## 📌 Pro Tips
- Use `--name` for easier container identification.
- Volumes ensure data persists beyond container lifespans.
- Use Dockerfiles to script your environment.
- Regular cleanup keeps Docker lightweight:

```bash
docker container prune
docker image prune
```
