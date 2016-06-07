+++
categories = ["x", "y"]
date = "2016-06-07T12:06:21+01:00"
section = ["key"]
slug = ["key"]
tags = ["x", "y"]
title = "Deploying a new Project"

draft=false

[menu.main]
	parent = "mn_dquickstart"
	weight = 2

+++

In order to deploy a new Docker project with your software you must follow this steps:

1. Clone our [Sandbox](https://github.com/BioDocker/sandbox) repository

2. Create a folder to your program with the necessary files following our [guidelines](https://github.com/BioDocker/specifications/wiki/Project-organization).

3. [Create a Dockerfile](https://github.com/BioDocker/specifications/wiki/Dockerfile-template) following the general guidelines.

4. Build the container in your own computer and test the image. If it works properly, then you may follow.

5. Push the container to your fork of our Sandbox and create an pull request following our contribution guidelines: 
 * https://github.com/BioDocker/biodocker/blob/master/CONTRIBUTING.md

 * If you can't do that, send a message to the <biodockers@gmail.com> so that we can help you adding your program.

6. Upon acceptance, we will create an <a href="https://docs.docker.com/docker-hub/builds/">automatic build</a> on DockerHub (this will allow people to search for the container using docker search).

7. Spread the news!