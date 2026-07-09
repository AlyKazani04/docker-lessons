# Bind Mounts and Volumes

Sometimes our containers need to be stateful in some capacity. Sometimes our containers need to read and write to the host. This is fundamentally at odds with the idea of a stateless, able-to-create-and-destroy-anytime container that we've been adhering to thusfar. So what are we to do?

Enter volumes and bind mounts. Both of these are methods of reading and writing to the host but with slight-but-important differences of when to use which.

## Bind Mounts

Bind mounts allow you to mount files from your host computer into your container. This allows you to use the containers a much more flexible way than previously possible: you don't have to know what files the container will have _when you build it_ and it allows you to determine those files _when you run it_.

> You can use the `nginx` container directly to test configurations and serve content directly from it.
> ```bash
>  # from the root directory of your Astro app (example)
> docker run --mount type=bind,source="$(pwd)"/dist,target=/usr/share/nginx/html -p 8080:80 nginx:latest
> ```
- `--mount` flag: to identify that something from the host will be mounted to the container.
- `bind` and `volume` are the two mount types we will talk about. We're using bind to mount in some piece of already existing data from the host.
- `source` and `target` both need to be absolute paths, hence `$(pwd)/dist` is used (to get the **P**resent **W**orking **D**irectory to make it an absolute path).
- The target is where we want those files to be mounted in the container. We're mounting it to `/usr/share/nginx/html`, which is what NGINX is expecting.

Again, it's preferable to bake your own container so you don't have to ship the container and the code separately; you'd rather just ship one thing that you can run without much ritual nor ceremony. But this is a useful trick to have in your pocket. It's kind of like serve but with real NGINX.

--- 
