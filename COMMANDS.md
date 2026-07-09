# Docker CLI Commands

## Image Management

Commands for working with Docker images (building, pulling, and viewing them).

| Command | Description | Useful Flags |
| --- | --- | --- |
| `docker build` | Build an image from a Dockerfile | `-t, --tag` : Name and tag the image (`name:tag`) |
| - | - | `-f, --file` : Specify the Dockerfile path |
| - | - | `--no-cache` : Do not use cache when building |
| `docker pull` | Download an image from a registry | `-a, --all-tags` : Download all tagged images in the repository |
| `docker images` | List local images | `-a, --all` : Show all images (including intermediate layers)
| - | - | `-q, --quiet` : Only show numeric IDs |
| `docker rmi` | Remove one or more images | `-f, --force` : Force removal of the image |
| `docker tag` | Create a tag targeting a source image | *None* |

> **Example: Building an image**
>
> ```bash
> docker build -t my-app:v1.0 .
> 
> ```

---

## Container Lifecycle

Commands to create, start, stop, and manage the life of containers.

| Command | Description | Useful Flags |
| --- | --- | --- |
| `docker run` | Create and start a new container | `-d, --detach` : Run container in background
| - | - | `-p, --publish` : Map ports (`host:container`)
| - | - | `-v, --volume` : Bind mount a volume (`host:container`)
| - | - | `--name` : Assign a name to the container
| - | - | `--rm` : Automatically remove the container when it exits
| - | - | `-e, --env` : Set environment variables |
| `docker ps` | List containers | `-a, --all` : Show all containers (default shows just running)
| - | - | `-q, --quiet` : Only display container IDs |
| `docker start` | Start one or more stopped containers | `-i, --interactive` : Attach container's STDIN |
| `docker stop` | Stop a running container | `-t, --time` : Seconds to wait before killing it (default 10) |
| `docker restart` | Restart a container | `-t, --time` : Seconds to wait before killing it |
| `docker rm` | Remove one or more containers | `-f, --force` : Force the removal of a running container
| - | - | `-v, --volumes` : Remove anonymous volumes associated with the container |

> **Example: Running a detached Nginx container**
>
> ```bash
> docker run -d -p 8080:80 --name web-server --rm nginx
> 
> ```
>
>

---

## Inspection & Debugging

Commands to look inside running containers and troubleshoot issues.

| Command | Description | Useful Flags |
| --- | --- | --- |
| `docker logs` | Fetch the logs of a container | `-f, --follow` : Follow log output

 `-n, --tail` : Number of lines to show from the end

 `-t, --timestamps` : Show timestamps |
| `docker exec` | Run a command in a running container | `-it` : Commonly used together for an interactive TTY session

 `-u, --user` : Username or UID |
| `docker inspect` | Return low-level information on Docker objects | `-f, --format` : Format the output using a Go template |
| `docker top` | Display the running processes of a container | *None* |
| `docker stats` | Display a live stream of container resource usage statistics | `--no-stream` : Disable streaming stats and pull only the first result |

> **Example: SSH-like access into a running container**
>
> ```bash
> docker exec -it web-server /bin/bash
> 
> ```

---

## Volumes & Networking

Commands to manage persistent data and communication paths.

### Volumes

* `docker volume ls` — List all local volumes.
* `docker volume create <volume_name>` — Create a new volume.
* `docker volume inspect <volume_name>` — Display detailed volume information.
* `docker volume rm <volume_name>` — Remove a volume.

### Networks

* `docker network ls` — List all networks.
* `docker network create <network_name>` — Create a new network (use `-d` to specify drivers like `bridge` or `overlay`).
* `docker network connect <network_name> <container>` — Connect a container to a network.
* `docker network disconnect <network_name> <container>` — Disconnect a container.

---

## System Cleanup

Docker can quickly eat up disk space with dangling images and stopped containers. These commands can help to clean up resources.

* `docker system df` — Show docker disk usage.
* `docker system prune` — Remove unused data.
* `-a, --all` : Remove all unused images, not just dangling ones.
* `--volumes` : Prune volumes as well (warning: this deletes persistent data!).
