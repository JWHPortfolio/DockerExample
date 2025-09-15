# [Nice Overview Site](https://dockerlabs.collabnix.com/docker/cheatsheet/)

# Look over existing images
### [RabbitMQ](https://hub.docker.com/_/rabbitmq)
### [MongoDB](https://hub.docker.com/r/mongodb/mongodb-community-server)
### [Neo4J](https://hub.docker.com/_/neo4j)

# DockerExample

## Example to create a docker build 

    $ docker build -t jhebeler/jwhregression:1.0 
    But builds only for your default architecture and places in your local (host) repository 
    $ docker build --platform linux/arm64 -t jhebeler/jwhregression:3.0 . 
    $ docker build --platform linux/arm64 -t jhebeler/jwhregression:3.0 . 
    $ docker push jhebeler/jwhregression:3.0 
    $ docker run jhebeler/jwhregression:1.0 
    $ docker run -v /home/jwh/workspace/DockerExample/output:output jhebeler/jwhregression:1:0

## for mulitple -  Warning after much toil counldn't get this to work!
    $ sudo docker buildx create --name mybuilder --driver docker-container --bootstrap
    $ sudo docker run --privileged --rm tonistiigi/binfmt --install all
    $ sudo docker buildx build -t jhebeler/jwhregression:2.0 .

## look in local repostiory
    $ sudo docker images>

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
