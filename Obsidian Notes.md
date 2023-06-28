## 1. Why Docker?
Allows seamless upgrades
	Without containers, an admin has to update every server and dependencies. With containers, you tell the _orchestrator_ you want to run a new *image version* and it gradually replaces every container with another one running the new version

Standardization for Containers
	When a machine runs the container image in which you have put your software, the container is created and the image is put inside. 

## Learning Centre Docker Desktop
The container display in Docker Desktop has 4 elements in the table: name, image, status and port(s)
By clicking in name you can access the log of the running of the container, as well as stopping it
By clicking in the port, you obtain the localhost link which will open in your browser

You will need to build your own Dockerfile
```Dockerfile
# Start your image with a node base image
FROM node:18-alpine

# The /app directory should act as the main application directory
WORKDIR /app

# Copy the app package and package-lock.json file
COPY package*.json ./

# Copy local directories to the current local directory of our docker image (/app)
COPY ./src ./src
COPY ./public ./public

# Install node packages, install serve, build the app, and remove dependencies at the end
RUN npm install \
    && npm install -g serve \
    && npm run build \
    && rm -fr node_modules

EXPOSE 3000

# Start the app using serve command
CMD [ "serve", "-s", "build" ]
```

To build in Docker we use the command     `docker build -t welcome-to-docker .
The -t flag tags your image with a name. (welcome-to-docker in this case). And the . lets Docker know where it can find the Dockerfile.

immediately an image is created inside docker desktop to the left menu. click on the name to see the details and once inside, click in run (top right corner) to run a new container w this image. 
Give a name and a port number such as 8089

immediately you are directed to a container that is running. the link will direct you to your browser localhost

to rename an image to your user change the prefix tag
`docker tag docker/welcome-to-docker YOUR-USERNAME/welcome-to-docker

what is a core? Processing unit of a CPU

## Basic Concepts


[[Containers]]: what we want to run and host in Docker, think of it as an isolated/virtual machine. A Docker server has several containers that run isolated from other containers and the host OS. Each container has its own ID so no prob confusing them even if they have the same name (possible if there is a test and release version)

[[Images]]: image describes everything needed to create a container, kind of like a template or a blueprint. All images are stored in a registry, being the default registry the Docker Hub