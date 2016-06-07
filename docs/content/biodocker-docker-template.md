+++
categories = ["x", "y"]
date = "2016-06-07T11:37:37+01:00"
section = ["key"]
slug = ["key"]
tags = ["x", "y"]
title = "Biodocker dockerfile template"
draft=false

[menu.main]
	parent = "mn_dquickstart"
	weight = 1
+++

# Biodocker dockerfile template

This is a standard template for creating a new Dockerfile for BioDocker:

> Note: Please always follow the [best practices](/biodocker-best-practices/) and help pages [Using input and Output files](/biodocker-input-output/) information.

Bellow is the complete example of a BioDocker Dockerfile:

```bash
#################################################################
# Dockerfile
#
# Version:          1
# Software:         Comet
# Software Version: 2015020
# Description:      basic local alignment search tool
# Website:          http://comet-ms.sourceforge.net/
# Tags:             Proteomics
# Provides:         Comet 2015020
# Base Image:       biodckr/biodocker
# Build Cmd:        docker build --rm -t biodckrdev/comet 2015020/.
# Pull Cmd:         docker pull biodckr/comet
# Run Cmd:          docker run --rm -it biodckrdev/comet <options> <files>
# Extra:            Extra information
# Extra:            with new lines if necessary
#################################################################

# Set the base image to biodocker base image
FROM biodckr/biodocker

################## BEGIN INSTALLATION ######################

# Change user to root
USER root

# UPDATE APT, INSTALL PREREQUISITES AND CLEAN CACHE
RUN apt-get clean all && \
    apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y wget && \
    apt-get clean && \
    apt-get purge && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# ADD FILES
ADD comet.2015020.linux.exe /home/biodocker/bin/

# RUN COMMANDS
RUN chmod +x /home/biodocker/bin/comet.2015020.linux.exe

# CHANGE USER BACK TO BIODOCKER
USER biodocker

# CHANGE WORKDIR TO /DATA
WORKDIR /data

# DEFINE DEFAULT COMMAND
CMD ["comet.2015020.linux.exe"]

##################### INSTALLATION END #####################

# File Author / Maintainer
MAINTAINER Felipe da Veiga Leprevost <felipe@leprevost.com.br>
# Modified by Yasset Perez-Riverol. 7edf3b0
```

## Header

Every Dockerfile must have a header with the following items:

- **Dockerfile Version**: This is a single-number version system (ex: v1, v2, v3 ...). Every change in the file must increase the version number in 1.

- **Software**: The name of the software installed inside the container. This can be a little tricky because some software demand libraries or dependencies. In this case the idea is to describe the "principal" software of the container, or the reason for built it.

- **Software Version**: The version of the software installed.

- **Description**:      Single line description of the tool

- **Website**:          URL(s) for the program developer separated by vertical bars (|)

- **Tags**: Program tags separated by vertical bars (|)
 
 - Genomics
 - Protemomics
 - Transcriptomics
 - Metabolomics
 - General

- **Provides**: List of programs provided separated by vertical bars (|)

- Base Image: All containers are based on a specific GNU/Linux system. There is no preference for a specific OS flavor but, to reduce disk usage, we recommend to use our own biodkr/biodocker image.

- Docker commands: Commands used to build, pull and run the docker image

- Extra: Extra information. this tag can appear multiple times

## Image Setting - FROM

The next element is the base image and any configuration to the system you are installing:

In the example above the Base Image is defined as biodckr/biodocker which is based on ubuntu latest LTS (Long Term Support) release and kept up to date with updates.

## Installation - RUN

The installation area is where you instructions to build the software will be defined. Here is the correct place to put Dockerfile syntax and system commands.

```bash
################### BEGIN INSTALLATION ########################

# Change user to root
USER root

# UPDATE APT, INSTALL PREREQUISITES AND CLEAN CACHE
RUN apt-get clean all && \
    apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y wget && \
    apt-get clean && \
    apt-get purge && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# ADD FILES
ADD comet.2015020.linux.exe /home/biodocker/bin/

# RUN COMMANDS
RUN chmod +x /home/biodocker/bin/comet.2015020.linux.exe

# Change user to back to biodocker
USER biodocker

# CHANGE WORKDIR TO /DATA
WORKDIR /data

# DEFINE DEFAULT COMMAND
CMD ["comet.2015020.linux.exe"]

#################### END INSTALLATION #########################
```

- Commands should be merged with '&& \' whenever possible in order to create fewer intermediate images.
- A biodocker user has been created (id 1001) so that applications are not run as root.
- If possible, add the program to /usr/bin, otherwise, add to /home/biodocker/bin
- return to the regular USER
- change the WORKDIR to the data folder
- set the VOLUMEs to be exported (/data and /config are exported by default by the base image)
- EXPOSE ports (if necessary)


## Signature - MAINTAINER

The File Author/ Maintainer signature. By default the Dockerfile only accepts one MAINTAINER tag. This will be the place the original author name. After updates are added to the file, the contributors name should appear in commented lines.

```
# File Author / Maintainer
MAINTAINER Felipe da Veiga Leprevost <felipe@leprevost.com.br>
# Modified by Yasset Perez-Riverol. 7edf3b0
```

The number after Yasset name is the 7 first digits of the commit.