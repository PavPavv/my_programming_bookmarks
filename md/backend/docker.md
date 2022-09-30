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

## Docker theory

### Main rules

Docker runs by Docker engine and create images with container. You can think of container like a mini-VM.
To run Docker you need a Dockerfile. Who has an image can create a containers. In Docker every Container should just do **one main** thing.

### Data in Docker

1. Application (read-only, stored in Images)
2. Temporary App Data (read/write, stored in Containers)
3. Permanent App Data (read + write, stored with Container & Volumes)

### Volumes

Volumes unlike Containers and Images hosts on a local machine. That means that data in Volumes survive Image or Container removing.

### Network

---

## Use Docker

1. To start using Docker you need a Dockerfile, like this:

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

## docker-compose

2. Then you can build an Image in the directory with Dockerfile:

```bash
docker build .
```

3. You can check an Image:

```bash
docker images
```

4. Create and start a new Container from an Image with detach publishing at the port of 3000 and remove after the stop with a certain name:

```bash
docker run -d -p 3000:80 --rm --name test-app
```

5. Check list of running Containers:

```bash
docker ps
```

6. Check list of all Containers:

```bash
docker ps -a
```

7. Stop the Container:

```bash
docker stop test-app
```

