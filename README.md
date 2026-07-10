# docker-lessons

### Lesson 1

## What are containers?

- The core of what containers are is just a few features of the Linux kernel duct-taped together to achieve isolation.

## Benefits of a container

- Security and resource-management features of VMs but without the cost of running a whole another OS.

## How they work

- They use chroot, namespaces and cgroups to separate a group of processes from each other.

### chroot

- Stands for 'Change Root'.
- It creates a separate environment for the users so they can't access the files of the host machine.

### Namespaces

- Namespaces allow you to hide processes from other processes.
- So users can't sent signals to other user's processes to sabotage them. (They get separate PIDs(process IDs))

### Cgroups

- Stands for 'Control Groups'.
- This allows us to govern how many resources each of the separate isolated environments can access.
- So no matter how bad a code some user is running, they won't be able to utilize more than, for example, 5% of the CPU.
- This also protects the host machine from resource exhaustion attacks like fork bombs within the containers.

---

## Notes
  
### [01 — Most Basic Dockerfile-Based Container](./01_most_basic_dockerfile-based_container/)  
Introduces the absolute basics of writing a `Dockerfile`. Pulls the `node:20` image from Docker Hub and runs a single `console.log` command via `CMD`. Demonstrates the `docker build` and `docker run` workflow.  
  
---  
  
### [02 — Basic Node Container](./02_basic_node_container/)  
Extends the basics by copying a local `index.js` file into the image using `COPY` and running it as a Node HTTP server on port 3000. Introduces key `docker run` flags: `--publish` (port mapping), `--init` (graceful shutdown with Ctrl+C), and `--rm` (auto-remove container on exit).  
  
---  
  
### [03 — WORKDIR Example](./03_workdir_example/)  
Introduces best practices for file organization and security inside a container. Demonstrates switching to a non-root `node` user with `USER`, setting a working directory with `WORKDIR`, and transferring file ownership with `COPY --chown`.  
  
---  
  
### [04 — Dependencies Example](./04_dependancies_example/)  
Shows how to handle npm dependencies inside a container. Uses `npm ci` to install from `package-lock.json`, introduces `.dockerignore` to exclude `node_modules` and other unnecessary files, and demonstrates running the container in interactive mode with `-it`.  
  
---  
  
### [05 — Build Time Optimization](./05_build_time_optimization/)  
Teaches Docker layer caching to speed up rebuilds. By copying `package.json` and `package-lock.json` first and running `npm ci` before copying the rest of the source files, Docker can skip the dependency installation step on subsequent builds when only application code has changed.  
  
---  
  
### [06 — Smaller Containers](./06_smaller_containers/)  
Demonstrates reducing image size by switching the base image from `node:20` (~1 GB) to `node:20-alpine` (~133 MB). Explains the trade-off: Alpine is preferred for production images, while the full distro is better for development due to its richer toolset.  
  
---  
  
### [07 — Custom Node Container](./07_custom_node_container/)  
Goes one step further by starting from a bare `alpine:3.19` image and manually installing Node.js and npm via `apk`. Also shows how to manually create a non-root `node` user and group when the base image doesn't provide one.  
  
---  
  
### [08 — Multi-Stage Image Build](./08_multi-stage_image_build/)  
Introduces multi-stage builds to produce lean production images. A full `node:20` image is used as a builder stage to install dependencies and prepare the app, then only the built output is copied into a minimal `alpine:3.19` image — resulting in a final image without npm or build tooling.  
  
---  
  
### [09 — Static Asset Project](./09_static_asset_project/)  
A real-world application of multi-stage builds. An Astro static site is built using a Node image (`npm run build`), and the compiled output from `dist/` is served by an `nginx:alpine` image — combining a JavaScript build tool with a production-grade web server in a single `Dockerfile`.  
  
---  
  
### [10 — Bind Mounts and Volumes](./10_bind_mounts_and_volumes/)  
Covers the two ways containers can interact with persistent or host-side data:  
- **Bind mounts** — mount existing files from the host into the container at runtime (e.g., serving a pre-built `dist/` folder with NGINX without rebuilding the image).  
- **Volumes** — Docker-managed file systems that persist data between container runs and can be shared across containers (e.g., an incrementing counter that survives restarts).

---

### [11 — Docker Networking](./11_docker_networking/)
A real-world example of networking using Docker containers. A Node server communicating with a MongoDB server running alongside it. Shows how Manual Bridge Networking can be implemented using Docker Containers.

---

### [12 — Docker Compose](./12_docker_compose/)
Docker Compose allows us the ability to coordinate multiple containers and do so with one YAML file. Docker Compose makes it really simple to define the relationship between these containers and get them all running with one `docker compose up`.