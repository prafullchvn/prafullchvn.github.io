---
title: 'Docker Basics'
date: 2023-02-26T17:19:46+05:30
draft: false
---

Docker is prime examle of platform which provides containerisation. There are mainy instances through which we can implement the containers but docker is one of the most popular to do so.

# Docker architecture

![Docker architecture](https://www.oreilly.com/api/v2/epubs/9781788992329/files/assets/7310b2e5-4a3d-4ee4-ad85-ee534de55540.png)

As you can see in picture, there are two main parts to the docker

1. docker CLI
2. docker server

We launch container, check their logs using docker CLI which in turns contacts docker server. Docker server is where docker daemon is running. Docker server is container runtime which runs all the container on top of it.

## Docker image

Docker image is a file which in turn is used to create the container. Docker image contains all the configuration that docker runtime need to create the container and launch the process inside of it.

## Snapshot of image

Suppose you have container running which have changed it's state over the period of time. Many changes might have come in it like change in configuration, change in files & change in platform etc. So suppose next you want to launch the same container but you want these changes to be there. In such case, you can save a snapshot of the container as image.

<!-- Steps to save the snapshot are yet to be put -->

## Dockerfile

You can use this file to create the image. There are certain commands which we need to put in it. Commands goes as follows

### `FROM`

This is where you specify the base image on top of which you will be putting your configuration.

Syntax:

```
FROM <image-name>[:<tag>]
```

### `WORKDIR`

This is used to specify the working directory inside of the container. If not present it will be created while execution.

Syntax

```
WORKDIR /path/to/workdir
```

### `ADD` or `COPY`

This is used to copy or add the files inside the container from host machine.
There is slight difference in ADD and COPY.
`ADD` here

#### `ADD`

Syntax

```
ADD <src> <dest>
```

Here src can be URL

#### `COPY`

The COPY instruction copies new files or directories from <src> and adds them to the filesystem of the container at the path <dest>.

Syntax

```
COPY <src> <dest>
```

Here both are the path of filesystem.

### `RUN`

- RUN <command> (shell form, the command is run in a shell, which by default is /bin/sh -c on Linux or cmd /S /C on Windows)
- RUN ["executable", "param1", "param2"] (exec form)

### `EXPOSE`

This command is used to expose the specific port of the container.

```
EXPOSE <port> [<port>/<protocol>...]
```

### `CMD`

The CMD instruction has three forms:

- `CMD ["executable","param1","param2"]` (exec form, this is the preferred form)
- `CMD ["param1","param2"]` (as default parameters to ENTRYPOINT)
- `CMD command param1 param2` (shell form)

The main purpose of a CMD is to provide defaults for an executing container. These defaults can include an executable, or they can omit the executable, in which case you must specify an ENTRYPOINT instruction as well.

NOTE: JSON array format is processed one by one. Shell feature of substitution for shell variable is not availble.

If the user specifies arguments to docker run then they will override the default specified in CMD.
