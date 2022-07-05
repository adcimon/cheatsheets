# Docker

<p align="center"><img align="center" src="assets/docker.svg"></p>

[Docker](https://www.docker.com/) is a set of platform as a service products that uses OS-level virtualization to deliver software in packages called containers.

## Index

* [General](#general)
* [Images](#images)
* [Containers](#containers)
* [Volumes](#volumes)
* [Networks](#networks)

## General

Check version.
```
docker version
```

## Images

List images.
```
docker image ls
docker image ls -a
```

Build an image base on a dockerfile.
```
docker image build -t <image> <path>
```

Tag an image.
```
docker image tag <image>:<tag> <target_image>:<tag>
```

Remove an image.
```
docker image rm <image>
```

Remove all images without a container.
```
docker image prune -a
```

## Containers

List containers.
```
docker container ls
docker container ls -a
```

Inspect a container.
```
docker container inspect <container>
```

List container port mappings.
```
docker container port <container>
```

Run a container.
```
docker container run <image>
```

Run a container and start an interactive shell.
```
docker container run -i -t <image> bash
```

Run a container, start an interactive shell and remove it on exit.
```
docker container run --rm -i -t <image> bash
```

Run a stopped container and start an interactive shell.
```
docker container start -a -i <container>
```

Execute a command inside a container.
```
docker container exec -i -t <container> <command>
docker container exec -i -t <container> bash
```

Fetch the logs of a container.
```
docker container logs <container>
docker container logs -f <container>
```

Stop a container.
```
docker container stop <container>
```

Kill a container.
```
docker container kill <container>
```

Remove a container.
```
docker container rm <container>
```

## Volumes

List volumes.
```
docker volume ls
```

Remove all unused volumes.
```
docker volume prune -f
```

## Networks

List networks.
```
docker network ls
```

Create a network.
```
docker network create <network>
docker network create --driver <driver> <network>
```

Connect a container to a network.
```
docker network connect <network> <container>
```

Disconnect a container from a network.
```
docker network disconnect <network> <container>
```
