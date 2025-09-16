# [Nice Overview Site](https://dockerlabs.collabnix.com/docker/cheatsheet/)

# Look over existing images in [Docker Hub](https://hub.docker.com/search?categories=Networking&categories=Message+queues) 
### [RabbitMQ](https://hub.docker.com/_/rabbitmq)
### [MongoDB](https://hub.docker.com/r/mongodb/mongodb-community-server)
### [Neo4J](https://hub.docker.com/_/neo4j)

# Other Repositories
### [Nvidia](https://catalog.ngc.nvidia.com/containers?filters=&orderBy=weightPopularDESC&query=&page=&pageSize=)
### [Tensorflow JupyterNotebook with GPU](https://docs.nvidia.com/deeplearning/frameworks/tensorflow-release-notes/running.html)
### [Azure ACR](https://azure.microsoft.com/en-us/products/container-registry)

## key options
    -v ties two files systems together.  Can use a host file system or shared file system
    -p exposes container port to host.  They do not have to be the same port

## Add shared file system - stored in a special area of your host machine (e.g., /var/lib/docker/volumes/ on Linux).
    $ docker volume create my-shared-data
    $ docker run -d --name container1 -v my-shared-data:/data <imageName1>
    $ docker run -d --name container2 -v my-shared-data:/data <imageName2> (could be same image but a different container)
    $ docker volume ls (list volumes)

## Add shared network
    $ docker network create my-app-network
    $ docker run -d --name container3 --network my-app-network <imageName>
    $ docker run -d --name container4 --network my-app-network <imageName>
    $ docker network ls (list networks)

# Docker Image Building Example
A Dockerfile is a text file containing instructions for building a Docker image. These instructions are processed sequentially, with each instruction creating a new layer in the image. Key parts of a Dockerfile include: 

• FROM: This instruction specifies the base image from which your new image will be built. It's the starting point for your image and typically defines the operating system and any pre-installed software. 

    FROM ubuntu:latest

• RUN: This instruction executes commands during the image build process. Each RUN instruction creates a new layer. It's used for tasks like installing packages, creating directories, or compiling code. 

    RUN apt-get update && apt-get install -y nginx

• WORKDIR: This instruction sets the working directory for any subsequent RUN, CMD, ENTRYPOINT, COPY, and ADD instructions. 

    WORKDIR /app

• COPY / ADD: These instructions copy files or directories from the build context (the local machine where the Dockerfile is located) into the image. COPY is generally preferred for simple file copying, while ADD offers more features like extracting compressed archives. 

    COPY . .

• EXPOSE: This instruction informs Docker that the container listens on a specified network port at runtime. It's purely for documentation and doesn't actually publish the port. 

    EXPOSE 80

• ENV: This instruction sets environment variables within the image. These variables are available to processes running inside the container. 

    ENV MY_VARIABLE="value"

• CMD: This instruction provides default commands or arguments for an executing container. There can only be one CMD instruction per Dockerfile. If an executable is not specified, ENTRYPOINT can define it. 

    CMD ["nginx", "-g", "daemon off;"]

• ENTRYPOINT: This instruction configures a container to run as an executable. It defines the primary command that will be executed when the container starts. CMD instructions provide default arguments to the ENTRYPOINT. 

    ENTRYPOINT ["java", "-jar"]

These instructions, along with others like VOLUME, USER, and LABEL, allow for the comprehensive definition of a Docker image's environment and behavior. 


## Example to create a docker build 

    $ docker build -t jhebeler/jwhregression:1.0 
    But builds only for your default architecture and places in your local (host) repository 
    $ docker build --platform linux/arm64 -t jhebeler/jwhregression:3.0 . 
    $ docker build --platform linux/arm64 -t jhebeler/jwhregression:3.0 . 
    $ docker push jhebeler/jwhregression:3.0 
    $ docker run jhebeler/jwhregression:1.0 
    $ docker run -v /home/jwh/workspace/DockerExample/output:output jhebeler/jwhregression:1:0

## for multiple -  Warning after much toil counldn't get this to work!
    $ sudo docker buildx create --name mybuilder --driver docker-container --bootstrap
    $ sudo docker run --privileged --rm tonistiigi/binfmt --install all
    $ sudo docker buildx build -t jhebeler/jwhregression:2.0 .

## look in local repostiory
    $ sudo docker images

## output to a remote image repository such as hub.docker.com 
    $ docker login 
    # and follow directions 
    $ docker push jhebeler/regression:1.0


Popular Base images to build an new docker image in the "from" clause in a dockerfile:

The FROM instruction in a Dockerfile specifies the base image for your new image. Choosing the right base image is crucial for factors like image size, security, and the availability of necessary tools and libraries. 
Here are some basic Docker images commonly used in the FROM clause: 

• Alpine: A very small, security-focused Linux distribution. It's often preferred for building minimal images, especially for compiled applications or those with few dependencies. 

    FROM alpine:latest

• Ubuntu: A popular and widely used Linux distribution, offering a balance between image size and the availability of a vast package repository. 

    FROM ubuntu:latest

• Debian: Another stable and well-supported Linux distribution, similar to Ubuntu in its package management and community support. 

    FROM debian:latest

• CentOS/Fedora: Red Hat-based Linux distributions, often chosen for enterprise environments or when specific Red Hat technologies are required. 

    FROM centos:latest

• Specific language runtimes: Official images provided for various programming languages, including pre-installed runtimes and development tools. Examples include: 
	• Node.js: 

        FROM node:lts-alpine

    Python. 
        FROM python:3.9-slim-buster

    java. 
        FROM openjdk:11-jre-slim

    go. 
        FROM golang:1.20-alpine

• Scratch: The smallest possible base image, essentially an empty image. It's used for building truly minimal images from scratch, typically for statically compiled binaries. 

    FROM scratch

Considerations when choosing a base image: 

    • Application requirements: The libraries and dependencies your application needs. 
    • Image size: Smaller images lead to faster builds, pulls, and reduced storage. 
    • Security: Minimal base images often have a smaller attack surface. 
    • Maintainability: Official images are generally well-maintained and regularly updated. 
    • Multi-stage builds: Utilize different base images for build and runtime stages to optimize the final image size. 


---
