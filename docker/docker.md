# Docker

<p align="center"><img align="center" src="docker.png"></p>

[Docker](https://www.docker.com/) is a set of platform as a service products that uses OS-level virtualization to deliver software in packages called containers.

## Images

List all images.
```
docker image ls
```

Remove an image.
```
docker image rm <name>
```

## Containers

List containers.
```
docker ps
docker ps -a
```

Inspect a container.
```
docker inspect <name>
```

Stop a container.
```
docker stop <name>
```

Kill a container.
```
docker kill <name>
```

Remove a container.
```
docker rm <name>
```

Fetch the logs of a container.
```
docker logs <name>
docker logs -f <name>
```