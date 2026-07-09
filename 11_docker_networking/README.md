# Manual Networking with Docker

Networking is the way how two or more docker containers can talk to each other.

### Why would we need two containers to communicate with each other? 

Imagine there's an **app** and a **database**. It's usually fine if the database is directly inside the container with the app, **if it's a small project**. But it would be easier if we could directly use a **Mongo** container running alongside the app. 

We are going to look at the simplest networking method:

## Bridge Networks

There is a default bridge network running all the time. You can check this out using `docker network ls`.

- The `bridge` network is the one that exists all the time and we could attach to it if we want to, but Docker recommends against it so we'll create our own. 
- There's also the `host` network which is the host computer itself's network.
- The last network with the `null` driver is one that you'd use if you wanted to use some other provider or if you wanted to do it manually yourself.

> Example of Creating a Network
> ```bash
> # create the network
> docker network create --driver=bridge app-net
> 
> # start a mongodb server
> docker run -d --network=app-net -p 27017:27017 --name=db --rm mongo:7
> ```

- Creating the Network
    - `create`: keyword to create the network.
    - `--driver`: what kind of network to use.
    - `app-net`: name of our network.
- Creating the DB server
    - `-d` or `--detach`: run this container in the background.
    - `--network`: set the network, the container needs to be connected to.
    - `-p` or `--port`: map the host machine's port to the container's port (`MongoDB`'s default port is `27017`).
    - `--name` flag: give a name to the container.
    - `--rm`: to toss/clean up the container's resource once done running.
    - `mongo:7`: is the container we are using, it's preconfigured with mongodb so it will make things easy for us.

## The Mongo App

The project files are available in [`mongo-app/`](./mongo-app/) directory, you can check them out to see how the project is implemented, if you want to. I won't be explaining how to build the Node API.

The [`Dockerfile`](./mongo-app/Dockerfile) is also the same as in previous lessons. We're just reading and writing to MongoDB now in the Node.js server, but we're using otherwise everything else the same.

> So build the container and run it using the following commands (inside `mongo-app/`):
> ```
> docker build --tag=my-mongo-app .
> docker run -p 8080:8080 --network=app-net --init --env MONGO_CONNECTION_STRING=mongodb://db:27017 my-mongo-app
> ```
- `-p` or `--port`: map the host machine's port to the container's port.
- `--network`: specify the network to connect the container to (Note: we are connecting to the network we created earlier, i.e; `app-net`).
- `--init` flag: This is so that the container respects outside signals to shut it down, via `Ctrl+C` for example, otherwise it will keep running.
- `--env` flag: This flag allows us to pass environment variables to the container.
    - `mongodb://db:27017`: `db` is the alias of the server, works just like `localhost` does.

After running this you can check this out on `http://localhost:8080` and the app should be working.