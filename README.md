# DockerExample
Example to create a docker build <br>

$ docker build -t jhebeler/jwhregression:1.0 .  # But builds only for your default architecture and places in your local (host) repository<br>
$ docker build --platform linux/arm64 -t jhebeler/jwhregression:3.0 .<br>
$ docker build --platform linux/arm64 -t jhebeler/jwhregression:3.0 .<br>
$ docker push jhebeler/jwhregression:3.0 <br>

# for mulitple<br>
    $ sudo docker buildx create --name mybuilder --driver docker-container --bootstrap<br>
    $ sudo docker run --privileged --rm tonistiigi/binfmt --install all<br>
    $ sudo docker buildx build -t jhebeler/jwhregression:2.0 .<br>

    # look in local repostiory<br>
    $ sudo docker images<br>

# output to a remote image repository such as hub.docker.com
$ docker login # and follow directions
$ docker push jhebeler/regression:1.0

[Nice Overview Site](https://dockerlabs.collabnix.com/docker/cheatsheet/)

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

AI responses may include mistakes.



---
