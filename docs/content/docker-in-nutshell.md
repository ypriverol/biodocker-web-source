+++
categories = ["x", "y"]
date = "2016-06-06T08:47:25+01:00"
section = ["key"]
slug = ["key"]
tags = ["x", "y"]
title = "Docker in NutShell"
draft=false

[menu.main]
	parent = "mn_docker"
	weight = 1

+++

# Docker in NutShell

Docker is an open platform for developing, shipping, and running applications. 
Docker is designed to deliver your applications faster. With Docker you can separate your applications from your
infrastructure. 

Docker does this by combining kernel containerization features with workflows and tooling that help you manage 
and deploy your applications. At its core, Docker provides a way to run almost any application securely isolated
in a container. The isolation and security allow you to run many containers simultaneously on your host. 

Docker’s container-based platform allows for highly portable workloads. Docker containers can run on a developer’s
local host, on physical or virtual machines in a data center, or in the Cloud.

<iframe width="560" height="315" src="https://www.youtube.com/embed/aLipr7tTuA4" frameborder="0" allowfullscreen></iframe>

## What are the major Docker components?

Docker has two major components:

- <a href="https://docs.docker.com/engine/quickstart/">Docker Engine</a>: the open source containerization platform.
- <a href="https://hub.docker.com">Docker Hub</a>: our Software-as-a-Service platform for sharing and managing Docker containers.

## What is Docker’s architecture?

Docker uses a client-server architecture. The Docker client talks to the Docker daemon, which does the heavy lifting of building,
running, and distributing your Docker containers. Both the Docker client and the daemon can run on the same system, or you can connect a Docker client to a remote Docker daemon.

## Docker Architecture Diagram

   <p style="text-align: center">
		<img alt="Layered Filesystems Diagram" src="/icons/figure2.svg">
   </p>
    <p>
       <ul>
        <li>The Docker daemon: As shown in the diagram above, the Docker daemon runs on a host machine.
            The user does not directly interact with the daemon, but instead through the Docker client.
        </li>
        <li>The Docker client: The Docker client, in the form of the docker binary, is the primary user interface to Docker. 
            It accepts commands from the user and communicates back and forth with a Docker daemon.
        </li>
        <li>Inside Docker: To understand Docker’s internals, you need to know about three resources:
            <ul>
             <li><a href="https://docs.docker.com/v1.8/userguide/dockerimages/">Docker images</a>:A Docker image is a read-only template. For example,
                 an image could contain an Ubuntu operating system with Apache and your web application installed.
                 Images are used to create Docker containers.
              </li>                         
              <li>Docker registries: Docker registries hold images. These are public or private stores from
                  which you upload or download images. The public Docker registry is provided with the Docker Hub.
              </li>
              <li><a href="https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/">Docker containers</a>: Docker containers are similar to a directory. A Docker container holds everything that
                  is needed for an application to run. Each container is created from a Docker image. Docker containers can 
                  be run, started, stopped, moved, and deleted.
              </li>
            </ul>
        </li>      
       </ul>
     </p>							

### How does a Docker image work?

We’ve already seen that Docker images are read-only templates from which Docker containers are launched. 
Each image consists of a series of layers. Docker makes use of union file systems to combine these layers into a single image.
Union file systems allow files and directories of separate file systems, known as branches, to be transparently overlaid, 
forming a single coherent file system.

One of the reasons Docker is so lightweight is because of these layers. When you change a Docker image—for example,
update an application to a new version— a new layer gets built. Thus, rather than replacing the whole image or entirely rebuilding,
as you may do with a virtual machine, only that layer is added or updated. Now you don’t need to distribute a whole new image,
just the update, making distributing Docker images faster and simpler.

Every image starts from a **Base image**, for example ubuntu, a base Ubuntu image, or fedora, a base Fedora image.
You can also use images of your own as the basis for a new image.

Docker images are then built from these base images using a simple, descriptive set of steps we call instructions. 
Each instruction creates a new layer in our image. Instructions include actions like:

- Run a command
- Add a file or directory
- Create an environment variable
- What process to run when launching a container from this image

These instructions are stored in a file called a Dockerfile. A **Dockerfile** is a text based script that contains instructions and commands for building the image from the base image. Docker reads this Dockerfile when you request a build of an image, executes the instructions, and returns a final image.

```bash

FROM biodckr/biodocker:latest

################## BEGIN INSTALLATION ###########################

USER biodocker

RUN ZIP=comet_binaries_2016012.zip && \ wget https://github.com/BioDocker/software-archive/releases/download/Comet/$ZIP -O /tmp/$ZIP && \ unzip /tmp/$ZIP -d /home/biodocker/bin/Comet/ && \ chmod -R 755 /home/biodocker/bin/Comet/* && \ rm /tmp/$ZIP
RUN mv /home/biodocker/bin/Comet/comet.2016012.linux.exe /home/biodocker/bin/Comet/comet
ENV PATH /home/biodocker/bin/Comet:$PATH

WORKDIR /data/

##################### INSTALLATION END ##########################

MAINTAINER Felipe da Veiga Leprevost <felipe@leprevost.com.br>

```

### How does a container work?

A container consists of an operating system, user-added files, and meta-data. As we’ve seen, each container is built from an image.
That image tells Docker what the container holds, what process to run when the container is launched, and a variety of other
configuration data. The Docker image is read-only. 

When Docker runs a container from an image, it adds a read-write layer on top of the image
(using a union file system as we saw earlier) in which your application can then run.

When you run a container, either by using the docker binary or via the API, the Docker client tells
the Docker daemon to run a container.

```bash
$ docker run -i -t ubuntu /bin/bash
```

>The Docker Engine client is launched using the docker binary with the run option running a new container. The bare minimum the
>Docker client needs to tell the Docker daemon to run the container is:

>What Docker image to build the container from, for example: **ubuntu**
>The command you want to run inside the container when it is launched, for example: **/bin/bash**

## References:

- [Understand Docker Architecture](https://docs.docker.com/engine/understanding-docker/)
- [Docker Tutorial - What is Docker & Docker Containers, Images, etc?](https://www.youtube.com/watch?v=pGYAg7TMmp0)
- [Docker Ecosystem](https://www.digitalocean.com/community/tutorials/the-docker-ecosystem-an-introduction-to-common-components)