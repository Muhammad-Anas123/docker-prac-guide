# 🐳 Docker Master Reference Guide
**By: Muhammad Anas**  
> A beginner-friendly, yet comprehensive documentation of Docker CLI commands and concepts, ideal for DevOps learners and revision.

---

## 📌 1. What Is Docker?

**Docker** is a platform that allows you to **build**, **package**, and **run applications in isolated environments** called containers. Containers are lightweight and portable, making it easy to run applications consistently across different environments.

### 📦 Why Use Docker?
- **Consistency**: Ensures identical environments from development to production.
- **Isolation**: Keeps applications and dependencies separate.
- **Portability**: Runs anywhere Docker is supported.
- **Efficiency**: Uses fewer system resources than VMs.

---

## ⚙️ 2. Docker Architecture Overview

```
Client  <-->  Docker Daemon  <-->  Docker Registry
   |                        |
   |                        +--> Containers (Running Apps)
   +--> Commands            +--> Images (App Blueprints)
```

- **Client**: Interface where you run Docker commands.
- **Docker Daemon**: Core service that manages containers and images.
- **Registry**: Stores Docker images (Docker Hub, Amazon ECR, etc.).
- **Images**: Templates used to create containers.
- **Containers**: Live, running instances of images.

---

## 🧰 3. Docker Setup and Installation

```bash
yum update -y
```
> Updates all system packages – ensures latest versions and security fixes.

```bash
sudo yum install docker -y
```
> Installs Docker using the `yum` package manager.

```bash
which docker
```
> Verifies Docker is installed and shows the path to its binary.

```bash
docker -v
```
> Displays the installed version of Docker.

```bash
service docker start
```
> Starts the Docker service so you can begin using Docker.

```bash
service docker status
```
> Shows whether the Docker daemon is running.

---

## ℹ️ 4. System Info & Container Overview

```bash
docker info
```
> Displays system-wide Docker details (containers, images, drivers, etc.).

```bash
docker ps
```
> Lists all currently running containers.

```bash
docker ps -a
```
> Lists all containers, including stopped ones.

```bash
docker images
```
> Lists all downloaded and created Docker images on your system.

---

## 🚀 5. Running Your First Container

```bash
docker run -it ubuntu /bin/bash
```
> Starts a new Ubuntu container interactively with a bash shell.

```bash
docker run -it --name anascontainer ubuntu /bin/bash
```
> Same as above but names the container `anascontainer` for easier reference.

---

## ⚙️ 6. Managing Docker Containers

```bash
docker start anascontainer
```
> Starts an existing container that has been stopped.

```bash
docker exec -it anascontainer bash
```
> Opens a bash shell inside the running `anascontainer`.

```bash
docker stop anascontainer
```
> Stops a running container gracefully.

```bash
docker rm anascontainer
```
> Removes a stopped container completely from the system.

---

## 🔍 7. Inspecting and Debugging

```bash
docker diff anascontainer
```
> Shows file system changes made inside the container.

```bash
history
```
> Lists the command history for the current shell session.

---

## 📸 8. Saving & Reusing Container Work

```bash
docker commit anascontainer updateimage
```
> Saves the state of the `anascontainer` as a new image named `updateimage`.

```bash
docker images
```
> Confirms the new image was created and available locally.

---

## 🧪 9. Creating Containers from Custom Images

```bash
docker run -it --name practicecontainer updateimage /bin/bash
```
> Creates and starts a new container from the saved `updateimage`.

---

## 🛠️ 10. Building Docker Images via Dockerfile

### Dockerfile Example
```Dockerfile
FROM ubuntu:latest
RUN echo "I am learning DevOps" > /tmp/testfile
```

```bash
docker build -t testimage .
```
> Builds an image named `testimage` from the current directory.

```bash
docker run -it --name testcontainer testimage /bin/bash
cat /tmp/testfile
```
> Starts a container from `testimage` and verifies the file inside it.

---

## 📦 11. Docker Volumes: Data Persistence

### Share Data Between Containers

```bash
docker run -it --name container1 myimage /bin/bash
# Inside container1
mkdir myvolume && cd myvolume && touch file1 file2 file3
```

```bash
docker run -it --name container2 --volumes-from container1 ubuntu /bin/bash
cd myvolume && ls
```
> Shares the volume from container1 to container2 – shows the same files.

### Mount Host Directory

```bash
docker run -it --name hostcontainer -v /home/ec2-user:/vida ubuntu /bin/bash
cd /vida && ls
```
> Mounts a directory from the host to the container – changes reflect both ways.

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
> Builds and runs a custom image with pre-included files and messages.

---

## 🧠 13. Summary: Most Useful Commands

| Command | Description |
|--------|-------------|
| `docker run -it image /bin/bash` | Create and run a container interactively |
| `--name containername` | Assign a name to a container |
| `docker start` / `stop` / `rm` | Manage container lifecycle |
| `docker exec -it name bash` | Access a running container |
| `docker ps -a` | View all containers (including stopped) |
| `docker images` | List available Docker images |
| `docker diff name` | Show file changes inside a container |
| `docker commit` | Save a container state as a new image |
| `docker build -t name .` | Build an image from a Dockerfile |
| `-v host:container` | Mount host volume to container |
| `--volumes-from name` | Share volumes between containers |
| `docker image/container prune` | Clean up unused resources |

---

## 📌 Pro Tips

- Use `--name` for readable container identification.
- Use volumes to persist data outside containers.
- Clean unused containers/images regularly:
```bash
docker container prune
docker image prune
```
