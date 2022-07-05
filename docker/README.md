# Docker

<p align="center"><img align="center" src="assets/docker.svg"></p>

[Docker](https://www.docker.com/) is a set of platform as a service products that uses OS-level virtualization to deliver software in packages called containers.

## Index

* [Images](#images)
* [Containers](#containers)
* [Networks](#networks)

## Images

List images.
```
docker image ls
docker image ls -a
```

Remove an image.
```
docker image rm <image>
```

## Containers

List containers.
```
docker container ls
docker container ls -a
```

Run a container.
```
docker container run <image>
```

Inspect a container.
```
docker container inspect <container>
```

Execute a command inside a container.
```
docker container exec -it <container> <command>
docker container exec -it <container> /bin/bash
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
