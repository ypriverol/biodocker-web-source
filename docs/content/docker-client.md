+++
categories = ["x", "y"]
date = "2016-06-06T20:58:39+01:00"
section = ["key"]
slug = ["key"]
tags = ["x", "y"]
title = "Learn about Docker Client"
draft=true

[menu.main]
	parent = "mn_docker"
	weight = 3

+++

# Learn about the Docker client

If you didn’t realize it yet, you’ve been using the Docker client each time you typed docker in your **Bash terminal**.
The client is a simple command line client also known as a command-line interface (CLI). Each action you can take with the
client is a command and each command can take a series of flags and arguments.

```bash
# Usage:  [sudo] docker [subcommand] [flags] [arguments] ..
# Example:
$ docker run -i -t ubuntu /bin/bash
```

You can see this in action by using the docker version command to return version information on the currently installed Docker client and daemon.

```bash
$ docker version
```

This command will not only provide you the version of Docker client and daemon you are using, but also the version of Go (the programming language powering Docker).

```bash
  Client:
  Version:      1.8.1
  API version:  1.20
  Go version:   go1.4.2
  Git commit:   d12ea79
  Built:        Thu Aug 13 02:35:49 UTC 2015
  OS/Arch:      linux/amd64

Server:
  Version:      1.8.1
  API version:  1.20
  Go version:   go1.4.2
  Git commit:   d12ea79
  Built:        Thu Aug 13 02:35:49 UTC 2015
  OS/Arch:      linux/amd64
```

## Get Docker command help

You can display the help for specific Docker commands. The help details the options and their usage.
To see a list of all the possible commands, use the following:

```bash
$ docker --help
```

To see usage for a specific command, specify the command with the --help flag:
```bash
$ docker attach --help

Usage: docker attach [OPTIONS] CONTAINER

Attach to a running container

  --help              Print usage
  --no-stdin          Do not attach stdin
  --sig-proxy=true    Proxy all received signals to the process
```  

>Note: For further details and examples of each command, see the command reference in this guide.