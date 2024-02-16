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

### Volumes (theory)

Volumes unlike Containers and Images hosts on a local machine. That means that data in Volumes survive Image or Container removing.

### Networks (theory)

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
docker build -t <your-image-name> .
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

### Networks

1. List on all the networks

```bash
sudo network ls
```

### Volumes

#### docker-compose

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
