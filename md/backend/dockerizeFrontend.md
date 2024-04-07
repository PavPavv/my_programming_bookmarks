# How to use Docker with React

## Add "Dockerfile" to the root of your project

## Describe "Dockerfile"

```bash
# Specify platform and it's version
FROM node

# Specify working directory
WORKDIR /app

# Copy main file with all of the dependencies for caching necessary
# in order not to run npm install every time we change the code base
COPY package.json .

# Install node_modules into the container
RUN npm install

# Copy rest of the code to the same container
# Every time we change the code we re-run COPY command of the Docker
COPY . .

EXPOSE 3000

CMD ["npm", "run", "dev"]
```

## Build Docker image from Dockerfile

Run in the project root directory (where is Dockerfile is placed) the following command
(Create named image)

```bash
docker build -t <your-image-name> .
```

Rebuild the image (the same exact command)

```bash
docker build -t <your-image-name> .
```

Check the list of Docker images:

```bash
docker images
```

Remove unnamed image (if you need so):

```bash
docker image rm <image-id>
```

> check out basic Docker cheat sheet: [https://github.com/PavPavv/my_programming_bookmarks/blob/main/md/backend/docker.md](https://github.com/PavPavv/my_programming_bookmarks/blob/main/md/backend/docker.md)

## Create Docker container from the image

Create and run named container with detach function and port from the image:

```bash
docker run -d -p 5173:5173 --name <your-container-name> <your-image-name>
```

Check all the running containers:

```bash
docker ps
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

### Hot refresh with Docker (Bind mounts)

**Bind mounts** have limited functionality compared to volumes. When you use a bind mount, a file or directory on the host machine is mounted into a container. The file or directory is referenced by its absolute path on the host machine. By contrast, when you use a volume, a new directory is created within Docker's storage directory on the host machine, and Docker manages that directory's contents.

The file or directory does not need to exist on the Docker host already. It is created on demand if it does not yet exist. Bind mounts are very performant, but they rely on the host machine's filesystem having a specific directory structure available.

Run the container with a special flags:

```bash
docker run -v your/local/directory:container/directory -d -p 5173:5173 --name <your-container-name> <your-image-name>
```

like:

```bash
docker run -v $(pwd)/src:/app/src -d -p 3000:5173 --name <your-container-name> <your-image-name>
```

Read only bind mount:

```bash
docker run -v $(pwd)/src:/app/src:ro -d -p 3000:5173 --name <your-container-name> <your-image-name>
```

```bash
docker run --env-file ./.env -v $(pwd)/src:/app/src:ro -d -p 3000:5173 --name <your-container-name> <your-image-name>
```

## Docker-compose

> Spacing matters!

1. Create _docker-compose.yml_ file

```yml
# Compose doesn't use version to select an exact schema to validate the Compose file, but prefers the most recent schema when it's implemented.
version: '3'
# Services represents in docker-compose docker containers
services:
  vite-react-app:
    # Specify an image for the service/container
    # In fact, we decompose docker terminal command, like:
    # docker run --env-file ./.env -v $(pwd)/src:/app/src:ro -d -p 3000:5173 --name <your-container-name> <your-image-name>
    # <your-image-name>
    build: .
    # -p 3000:5173
    ports:
      - '3000:5173'
    # -v $(pwd)/src:/app/src
    volumes:
      - ./src:/app/src
    # -e VITE_APP_NAME=pavpav
    # environment:
    #   - VITE_APP_NAME=pavpav
    # --env-file ./.env
    env_file:
      - ./.env
```

2. Run the target containers by running docker-compose:

```bash
docker-compose up -d
```

If you want to rebuild image:

```bash
docker-compose up -d --build
```

3. Stop containers:

```bash
docker-compose down
```

4. Run several docker-compose files for many containers:

```bash
sudo docker-compose -f docker-compose.yml -f docker-compose-prod.yml up -d --build
```
