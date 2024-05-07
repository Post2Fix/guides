
# Docker

## Getting Started

- Install [Docker]

- Verify installation:

```bash 
docker version # full description of docker version
docker -v # short description of docker version
docker info # system wide information
docker run hello-world # run a test container
```

### Optional Post Installation Steps
```bash
# 1. Add your user to the docker group (run docker without sudo)
sudo usermod -aG docker $USER 
```
2. Log out and log back in so that your group membership is re-evaluated.

3. Verify that you can run docker commands without sudo.

## Docker Commands

**Images**

```bash
docker search <image_name> # Search Docker Hub for images.
docker pull <image_name> # Pull an image from a registry
docker imagee # List downloaded images
docker build -t <image_name> . # Build an image from a Dockerfile
docker rmi <image_name> # Remove an image.
docker tag <image_name> <new_repository>/<new_name> # Tag an image (often used before pushing to a different registry).
```


Absolutely! Here's each section formatted with Bash code blocks to highlight the commands distinctly:

**Containers**
```bash
docker run <image_name> # Basic container creation
docker run -d <image_name> # Run in detached mode
docker run -it <image_name> <command> # Interactive mode with TTY
docker ps # List running containers
docker ps -a # List all containers
docker stop <container_id_or_name> # Stop a container
docker start <container_id_or_name> # Start a stopped container
docker rm <container_id_or_name> # Remove a stopped container
docker exec -it <container_id_or_name> <command> # Execute command in container
```

**Networking**
```bash
docker run -p <host_port>:<container_port> <image_name> # Expose port
docker network ls # List networks
docker network create <network_name> # Create network
docker network connect <network_name> <container_name> # Connect container to network
```

**Volumes**
```bash
docker run -v <host_path>:<container_path> <image_name> # Mount host directory as volume
docker volume ls # List volumes
docker volume create <volume_name> # Create volume
docker volume inspect <volume_name> # Get volume details
```

**Dockerfile**
```bash
FROM <base_image> # Base image
RUN <command> # Execute commands
COPY <source> <destination> # Copy files
WORKDIR <path> # Set working directory
ENV <key>=<value> # Set environment variable
CMD <command> <param1> <param2> # Default command (exec)
ENTRYPOINT ["<command>", "<param1>", "<param2>"] # Default command (list)
LABEL <key>=<value> # Add metadata
EXPOSE <port> # Expose port
ADD <src> <dest> # Add files/URLs
COPY <source> <destination> # Copy files/directories
USER <user_uid> # Set user/UID
```

**Docker Hub**
```bash
docker login # Login to Docker Hub
docker push <username>/<image_name> # Push image to Docker Hub
```

**Docker Compose**
```bash
docker-compose up -d # Start services
docker-compose down # Stop and remove services
docker-compose ps # List Compose project containers
```

**Cleanup**
```bash
docker system prune # Remove unused data (safe)
docker system prune -a # Remove ALL unused data (caution)
```

Each block is now enclosed in Bash formatting for clarity and ease of reference.

  
Here is the reformatted version of the provided Docker commands documentation using Bash code blocks to clearly separate commands from comments, and organizing titles effectively:

## Running Containers

### Run hello-world container
```bash
docker run hello-world # Run 'hello-world' to test basic container setup
```

### Run an Alpine container
- **Search for an image and display summary**
```bash
docker search alpine --filter=stars=1000 --no-trunc # Search for 'alpine' with at least 1000 stars, display full text
```
- **Fetch Alpine image from Docker registry**
```bash
docker pull alpine # Download 'alpine' image from Docker registry
```
- **Display list of local images**
```bash
docker image ls # List downloaded images
```
- **List container contents using listing format**
```bash
docker run alpine ls -l # Run 'ls -l' inside the 'alpine' container
```
- **Print message from container**
```bash
docker run alpine echo "Hello from Alpine!" # Print a greeting message from 'alpine'
```
- **Attach container to an interactive tty**
```bash
docker run -it alpine bin/sh # Start an interactive shell in 'alpine'
```

## Creating Images

### Create custom image with GIT setup
- **Create project folder with empty Dockerfile**
```bash
cd ~
mkdir -p projects/docker/alpine-git
cd projects/docker/alpine-git
touch Dockerfile # Setup a new Docker project folder and create a Dockerfile in it
```
- **Edit the Dockerfile**
```bash
# Dockerfile setup for custom 'alpine' image with Git and Vim
FROM alpine:latest
LABEL author="codesaucerer" description="Official Alpine image with GIT and VIM installed"
ENV WORKING_DIRECTORY=/projects
RUN apk update && apk add git vim # Install Git and Vim on Alpine
RUN mkdir $WORKING_DIRECTORY # Create a working directory
WORKDIR $WORKING_DIRECTORY # Set the working directory
```
- **Build the Dockerfile**
```bash
docker image build -t [docker-username]/alpine-git . # Build the image from Dockerfile
docker run --rm -it [docker-username]/alpine-git /bin/sh # Run and enter the newly built image
```
- **Push the image to Docker Hub**
```bash
docker login # Login to Docker Hub
docker push [docker-username]/alpine-git:latest # Push the custom image to Docker Hub
```

This approach ensures each step is clear and concise, with the use of Bash blocks to separate commands, enhancing readability and accessibility.
  

---
[Docker]:https://docs.docker.com/engine/installation/

[free training]: https://training.docker.com

[repository]: https://hubs.docker.com

**Remember, practice makes perfect!**
