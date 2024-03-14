# Docker Compose Nodejs and MongoDB example

## Run the System
We can easily run the whole with only a single command:
```bash
docker compose up
```

Docker will pull the MongoDB and Node.js images (if our machine does not have it before).

The services can be run on the background with command:
```bash
docker compose up -d
```

## Stop the System
Stopping all the running containers is also simple with a single command:
```bash
docker compose down
```

If you need to stop and remove all containers, networks, and all images used by any service in <em>docker-compose.yml</em> file, use the command:
```bash
docker compose down --rmi all
```

# To use Docker Compose to build a Docker image
you can define a service in your docker-compose.yml file with the build option pointing to the Dockerfile's directory. Here's an example:

#### Create a Dockerfile:

Create a **Dockerfile** in your project directory with instructions on how to build your Docker image. For example:
```Dockerfile
FROM nginx:latest
COPY nginx.conf /etc/nginx/nginx.conf
```

#### Create a Docker Compose file:

Create a **docker-compose.yml** file in your project directory and define your service. Here's an example:

```yaml
version: '3'
services:
    web:
      build: .
      ports:
        - "8080:80"
```

This **docker-compose.yml** file defines a service named "web" that builds the Docker image using the Dockerfile in the current directory (.) and exposes port 8080 on the host, forwarding requests to port 80 in the container.

#### Build the Docker Image:

Run the following command in the same directory where your docker-compose.yml file is located:

```bash
docker-compose build
```

This command will build the Docker image according to the instructions in the Dockerfile.

####    Run the Docker Image:

After the image is built, you can run it using Docker Compose:

```bash
docker-compose up
```

This command will start the container based on the image you built.



# Docker-compose Push

The docker-compose push command is used to push Docker images to a Docker registry, such as Docker Hub or a private registry. It is a subcommand of Docker Compose, a tool for defining and running multi-container Docker applications.

When you run docker-compose push, it iterates over all services defined in your docker-compose.yml file and pushes the corresponding images to the registry. Each service's image name and tag are defined in the image field of the service definition.

Here's a breakdown of how the docker-compose push command works:

####    Service Definitions:
    
The docker-compose.yml file defines one or more services, each specifying an image name and tag to be pushed to the registry. For example:

```yaml
version: '3'

services:
  web:
    image: your-username/your-image:latest
```

#### Build and Tag Images:
If the image specified in the service definition is not already available locally, Docker Compose will build it based on the Dockerfile in the service's directory and tag it according to the specified image name and tag.

#### Push Images:
Once all necessary images are built and tagged, Docker Compose pushes each image to the registry specified in the image name.

#### Authentication:
Docker Compose requires authentication to push images to a Docker registry. You need to be logged in to the registry using docker login before running docker-compose push.

#### Parallel Pushing:
By default, Docker Compose pushes images in parallel, which can speed up the process, especially for projects with multiple services.