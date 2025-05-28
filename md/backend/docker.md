# Cheat sheet: Docker

## In which language Docker is written?

- Go

---

## Run Docker

Check is Docker installed in Linux:

```bash
docker --version
```

Check if Docker enabled in Linux system:

```bash
sudo systemctl status docker
```

Run docker in Linux

```bash
systemctl start docker
```

Stop docker in Linux

```bash
systemctl stop docker
```

---

## Docker basic theory

### Main rules

Docker runs by Docker engine and create images with containers. You can think of container like a mini-VM.
To run Docker you need a Dockerfile. Who has an image can create a containers. In Docker every container should just do **one main** thing.

### Data in Docker

1. Application (read-only, stored in Images)
2. Temporary App Data (read/write, stored in Containers)
3. Permanent App Data (read + write, stored with Container & Volumes)

### Images (theory)

In Docker, an image is a lightweight, standalone, and executable package that includes everything needed to run a piece of software, including the code, runtime, libraries, environment variables, and configuration files. Think of it as a template or blueprint for creating a live instance known as a container.

### Containers (theory)

In Docker, containers can be run in two main modes: attached mode and detached mode.

Attached mode.
When you run a Docker container in attached mode, your terminal session is directly connected to the container's standard input (stdin), standard output (stdout), and standard error (stderr). This means that you can see the output of the application running inside the container in real-time, and you can interact with it directly through your terminal. In this case, if you run a container interactively, you would typically use the -it flags (interactive and TTY).

Detached Mode
In detached mode, the container runs in the background, and you do not have a direct connection to its standard input or output. This mode is useful for running long-lived processes that do not require interactive user input, such as web servers or background tasks.
To run a container in detached mode, you use the -d flag.

The **docker run** command is used to create and start a new container from a specified image. It not only starts the container but also creates it in the process if it doesn’t already exist. When you run **docker run**, you can specify a variety of options such as environment variables, port mappings, volume mounts, and more. Once executed, a new container instance is created and started.

Purpose: The **docker start** command is used to start an existing, stopped container. It does not create a new container; instead, it starts a container that has been previously created but is in the stopped state. This command will start the container with the same settings and state it was in when it was stopped (including any internal state, process, etc.). Use **docker start** when you want to restart a container that is already created and configured, without changing its existing settings.

Request to outer servers are always possible in containers. Request to the local machine servers and other containers possible in Docker via networks.

### Volumes (theory)

Volumes unlike Containers and Images hosts on a local machine. That means that data in Volumes survive Image or Container removing.
A Docker-managed storage mechanism that is completely managed by Docker. They are stored in a part of the host filesystem that is managed by the Docker daemon (/var/lib/docker/volumes/ on Linux systems). Created, listed, and managed using Docker CLI commands (**docker volume create**, **docker volume ls**, etc.). Docker takes care of the lifecycle of volumes.
Best for shared data between containers and scenarios where you need to keep data after a container is deleted. Volumes are preferred when you want data to persist beyond the lifecycle of the container.
Generally provide better performance since they are optimized for Docker and can take advantage of Docker's storage drivers.
Volumes offer better isolation since they are controlled by Docker, and their contents do not depend on or automatically change with the host’s filesystem.

### Bind Mounts (theory)

Development only! In production we always want a snapshot of our code!

A way to specify a host directory or file to use as a mount point inside the container. The directory or file must exist on the host, and it can be located anywhere in the filesystem. Managed by the host operating system, and changes made to files in a bind mount are reflected immediately in both the host and container.
Useful for development environments where you want to have direct access to the files on your host system. For example, you might want to mount a local directory into a container to see changes in real-time without rebuilding the container.
Performance can depend on the underlying host filesystem and how Docker interacts with it, which may be less optimal than using volumes.
Bind Mounts can potentially lead to issues with differences in file permissions and configurations on the host, since they directly map to the host's filesystem.

To create a bind mount in Docker, you can use the -v or --mount option when you run a container. You can create a bind mount using the -v option. The basic syntax is:

```bash
docker run -v /host/path:/container/path <image>
```

Alternatively, you can use the more explicit --mount flag, which provides more options for configuring the mount.

```bash
docker run --mount type=bind,source=/host/path,target=/container/path <image>
```

**docker run** command here start the container with volume mounts and port mappings for local Node.js development:

```bash
docker run -d \                 # Run the container in detached mode
  --name <container-name> \     # Name the container
  -v $(pwd):/app \              # Mount the current directory to /app
  -v /app/node_modules \        # Preserve node_modules in the container
  -p 3000:3000 \                # Map port 3000 on host to port 3000 in the container
  <image-name>                  # Use the built image
```

### Networks (theory)

Use networks to communicate between multiple container. Sending http requests from the container to the outside works by default.

### Deploy

#### Things to watch out for

- **Bind Mounts** should not be used in Production!
- Containerized apps might need a build step (frontend mostly)
- Multi-container projects might need to be split (or should be split) across multiple hosts/remote machines (docker-compose)
- Use **COPY** to copy a code snapshot into the image
- Stages can copy results (created files and folders) from each other
- You can either build the complete image or select individual stages

---
---

## Use Docker

## Describe "Dockerfile"

To start using Docker you need to create a Dockerfile at your project root folder, like this:

```Dockerfile
# Inheritance
FROM node:14

# Initialization
WORKDIR /app
COPY package.json
RUN npm install
COPY . .

# Commands
EXPOSE 80

# Initialization
VOLUME ["app/test"]

# Commands
CMD ["node", "server.js"]
```

### Images

Then you can build an Image in the directory with Dockerfile:

```bash
docker build .
```

(Create named image)

```bash
docker build -t <your-image-name>:<your-image-tag> .
```

Rebuild the image (the same exact command)

```bash
docker build -t <your-image-name> .
```

You can check all the images:

```bash
docker images
```

```bash
sudo docker image ls
```

```bash
# only id's
sudo docker image ls -q
```

Delete all the images

```bash
sudo docker image prune
```

Delete all the stopped images

```bash
sudo docker image prune -a
```

Delete chosen image

```bash
sudo docker rmi imageIdOrName
```

### Containers

Create and start a new Container from an Image with detach publishing at the port of 3000 and remove after the stop with a certain name:

```bash
docker run -d -p 3000:80 --name <your-container-name> <your-image-name>
```

Check list of running Containers:

```bash
docker ps
```

Check list of all Containers:

```bash
docker ps -a
```

Stop the Container:

```bash
docker stop test-app
```

Kill a running container if you need so:

```bash
docker rm <you-container-name> -f
```

Get into the container's shell

```bash
docker exec -it <your-container> sh
```

Get out from the container's shell

```bash
exit
```

Delete all the stopped containers

```bash
sudo docker container prune
```

```bash
docker run --env-file ./.env -v $(pwd)/src:/app/src:ro -d -p 3000:5173 --name <your-container-name> <your-image-name>
```

### Volumes

You can create a Docker volume using the docker volume create command. The basic syntax is:

```bash
docker volume create <volume_name>
```

To use the volume in a Docker container, you can specify it with the -v or --mount option when running the container.

```bash
docker run -v <volume_name>:/container/path <image>
```

or 

```bash
docker run --mount type=volume,source=<volume_name>,target=/container/path <image>
```

### Networks (Container networks)

1. List on all the networks

```bash
sudo network ls
```

2. Run network from terminal

```bash
sudo docker network create some-net-name
sudo docker run -d --name container-name --network some-net-name image-name
# add another container to the same network
sudo docker run --name another-container-name --network some-net-name -d --rm -p 3000:3000 another-image-name
```

3. Multiple containers for server and database

Dockerfile for server:

```Dockerfile
FROM node:20-alpine

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

CMD ["node", "app.js"]
```

---
---

### docker-compose

```yaml
version: '3.8'

services:
  service_one:
    image: some-image:latest
    build:
      context: .
      dockerfile: ./some/some/Dockerfile
    container_name: some_name
    expose:
      - '3000'
    working_dir: /someDir
    command: 'yarn build'
    restart: on-failure
  service_two:
    context: .
    dockerfile: ./some/some/Dockerfile
  service_three:
    context: .
    dockerfile: ./some/some/Dockerfile
```

1. Version of docker-compose

```bash
sudo docker-compose version
```

1. Help with all the commands

```bash
sudo docker-compose
```

2. Build or rebuild services

```bash
sudo docker-compose build
```

3. Create services

```bash
sudo docker-compose create
```

4. Restart services

```bash
sudo docker-compose restart
```

5. Stop services

```bash
sudo docker-compose stop
```

5. Create and start containers

```bash
sudo docker-compose up
```

Detach mode: run containers in the background (with no logs)

```bash
sudo docker-compose up -d
```

6. List of images

```bash
sudo docker-compose images
```

7. List of containers

```bash
sudo docker-compose ps
```

8. Remove stopped containers

```bash
sudo docker-compose rm
```

5. Run several docker-compose files for many containers:

```bash
sudo docker-compose -f docker-compose.yml -f docker-compose-prod.yml up -d --build
```
