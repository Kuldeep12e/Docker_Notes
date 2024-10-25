# Docker Overview

## Definition of Docker
Docker is an open-source platform that automates the deployment, scaling, and management of applications in containers. Containers package up the application with all its dependencies, libraries, and configuration files, ensuring consistency across different environments.

## Images
An **image** is a snapshot or blueprint of a complete environment for an application. It includes everything the application needs to run, such as library dependencies, configurations, etc. Images encapsulate the app and all requirements together.

## Containers
A **container** is an actual instance of the environment configured by an image when we run it. When a Docker image is executed, it creates a live and running container. Containers are isolated and lightweight, sharing the host kernel, making them different from virtual machines (VMs).

## Benefits
- Applications behave consistently across any operating system where the container is run.
- Containers are isolated from the host machine’s dependencies.
- All containers remain isolated from one another, promoting security and modularity.

---

# Docker Commands Cheat Sheet

This README provides a collection of commonly used Docker commands along with their descriptions and uses, including extra notes for clarity.


docker volume create node_modules
# Creates a named volume for persistent storage of node_modules.
# Use this volume to ensure dependencies persist across container restarts.

docker run -it -v node_modules:/app/node_modules <image_name>
# Mounts the node_modules volume into the /app/node_modules directory of the container.
# This allows for persistent storage of Node.js dependencies.



# Docker Commands Cheat Sheet

This README provides a collection of commonly used Docker commands along with their descriptions and uses, including extra notes for clarity.

## Basic Commands

### Pull an Image
```bash
docker pull <image_name>
# Downloads a Docker image from a registry (like Docker Hub) to your local machine.
# Example: docker pull ubuntu
```

### Run an Interactive Container
```bash
docker run -it <image_name>
# Starts a new container from the specified image and opens an interactive terminal.
# The '-it' flag allows you to interact with the container via the terminal.
```

### List Running Containers
```bash
docker ps
# Displays a list of currently running containers.
# Add '-a' to see all containers, including stopped ones: docker ps -a
```

### Prune Unused Images
```bash
docker image prune
# Removes all dangling images (images not associated with any container).
# Use '--all' to remove all unused images: docker image prune --all
```

### Run a Container and Automatically Remove it on Exit
```bash
docker run -it --rm <image_name>
# Runs a container and automatically removes it when it stops.
# Useful for temporary containers that you don't need to keep.
```

### Run a Detached Container
```bash
docker run --detach -it <image_name>
# Starts a container in detached mode (in the background).
# You can view logs and attach to it later if needed.
```

### Attach to a Running Container
```bash
docker attach <container_name_or_id>
# Attaches your terminal to a running container.
# Useful for accessing the main process of the container.
```

### Run Command in a Container (Correction)
```bash
docker run <image_name>
# Starts a container from the specified image.
# Note: This command will run the default command defined in the image.
```

### Kill a Running Container
```bash
docker kill <container_name_or_id>
# Sends a SIGKILL signal to a running container, forcefully stopping it.
# Use this if a container is not responding to a normal stop command.
```

### Run a Container with a Custom Name
```bash
docker run -it --detach --name <custom_name> <image_name>
# Runs a container with a specified name, making it easier to reference later.
# Example: docker run -it --detach --name my_container ubuntu
```

### Run a Detached Container (Correction)
```bash
docker run -dit <image_name>
# Starts a container in detached mode and allocates a pseudo-TTY.
# Useful for running background services.
```

### Run Node in a Container
```bash
docker run -it node bash
# Runs a Node.js container and opens a bash shell.
# This is useful for testing Node.js applications interactively.
```

### Inspect an Image
```bash
docker inspect <image_name_or_id>
# Provides detailed information about an image or container, including configuration, environment variables, and networking details.
```

### Pause a Container
```bash
docker pause <container_id>
# Pauses all processes in a running container.
# Use this if you want to temporarily halt a container without stopping it.
```

### Unpause a Container
```bash
docker unpause <container_id>
# Unpauses a previously paused container, resuming its processes.
```

### Execute Command in a Running Container
```bash
docker exec -it <container_id> bash
# Opens an interactive bash shell in a running container.
# This allows you to run commands directly inside the container.
```

### Remove an Image (Correction)
```bash
docker rmi <image_id>
# Removes a Docker image from your local machine.
# Use this to free up space, but ensure no containers are using the image.
```

### Build an Image from Dockerfile
```bash
docker build .
# Builds a Docker image using the Dockerfile in the current directory.
# Ensure your Dockerfile is properly configured for building the image.
```

### Build an Image with a Tag
```bash
docker build -t <tag_name> .
# Builds a Docker image with a specific tag.
# Tags help you identify different versions of an image easily.
```

### Run a Container with Init System
```bash
docker run -it --init <image_name>
# Runs a container using an init system to manage processes.
# This helps to handle zombie processes and other PID 1 issues.
```

### Publish Ports on Run
```bash
docker run -it --init --publish 3000:3001 <image_name>
# Maps a host port to a container port, allowing you to access services running in the container from your host.
# Example: access a web service running on port 3001 inside the container via localhost:3000.
```

### Clean Up System
```bash
docker system prune -a
# Cleans up unused containers, images, and networks.
# Be cautious as this command can delete a lot of data. Use it to free up disk space.
```

### Build an Image from a Specified Dockerfile
```bash
docker build -t <tag_name> <path_to_dockerfile>
# Builds an image using a Dockerfile located at a specified path.
# This is useful if your Dockerfile is not in the current directory.
```

### Run a Container with Port Binding
```bash
docker run -it --init -p <host_port>:<container_port> <image_name>
# Maps host port to container port when running a container.
# This allows you to access the application inside the container from your local machine.
```

### Bind Mount a Project with Docker Container
```bash
docker run -it --init -p 3002:3000 -v "$(pwd)":/developer/nodejs/node-bind-mount-project <image_name>
# Binds the current directory to a path in the container.
# This is useful for development, allowing you to edit files locally and have them reflect in the container.
```

### Login to Docker Hub
```bash
docker login
# Authenticates your Docker client to your Docker Hub account.
# Required before pushing images to your Docker Hub repository.
```

### Tag an Image for Pushing
```bash
docker tag <source_image> <repository/image_name>
# Tags an image so it can be pushed to a remote repository.
# Use this to prepare your images for sharing with others.
```

### Push an Image to Docker Hub
```bash
docker push <repository/image_name>
# Uploads a tagged image to Docker Hub.
# Make sure you have the right permissions to push to the specified repository.
```

## Unique Commands

### View Logs of a Container
```bash
docker logs <container_name_or_id>
# Displays the logs for a specific container.
# Useful for debugging and understanding what’s happening inside the container.
```

### Stop a Running Container Gracefully
```bash
docker stop <container_name_or_id>
# Stops a running container by sending a SIGTERM signal, allowing it to shut down cleanly.
```

### Remove a Stopped Container
```bash
docker rm <container_name_or_id>
# Removes a stopped container from the local machine.
# You cannot remove a running container without stopping it first.
```

### View Resource Usage
```bash
docker stats
# Displays real-time statistics for running containers, including CPU and memory usage.
# Helps in monitoring resource consumption.
```

### Docker Compose (if applicable)
```bash
docker-compose up
# Starts and runs all services defined in a docker-compose.yml file.
# This command simplifies running multi-container applications.
```

Feel free to modify this document as per your learning journey!
