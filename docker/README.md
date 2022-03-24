# Docker

<p align="center"><img align="center" src="assets/docker.png"></p>

[Docker](https://www.docker.com/) is a set of platform as a service products that uses OS-level virtualization to deliver software in packages called containers.

## Index

* [Images](#images)
* [Containers](#containers)

## Images

List all images.
```
docker image ls
```

Remove an image.
```
docker image rm <image>
```

## Containers

List containers.
```
docker ps
docker ps -a
```

Run a container.
```
docker run <image>
```

Inspect a container.
```
docker inspect <container>
```

Execute a command inside a container.
```
docker exec -it <container> <command>
docker exec -it <container> /bin/bash
```

Fetch the logs of a container.
```
docker logs <container>
docker logs -f <container>
```

Stop a container.
```
docker stop <container>
```

Kill a container.
```
docker kill <container>
```

Remove a container.
```
docker rm <container>
```
