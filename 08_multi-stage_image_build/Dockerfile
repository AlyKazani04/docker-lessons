# build step
FROM node:20 AS node-builder
RUN mkdir /build
WORKDIR /build
COPY package*.json ./
RUN npm ci
COPY . .

# build step uses node configured distro to build the application and install dependancies
# makes a build directory
# set the working directory to it
# copy package info files to this dir
# install dependancies using npm
# copy rest of the files to this dir 
# this is not the final image

# production step
FROM alpine:3.19
RUN apk add --update nodejs
RUN addgroup -S node && adduser -S node -G node
USER node
RUN mkdir /home/node/code
WORKDIR /home/node/code
COPY --from=node-builder --chown=node:node /build .
CMD ["node", "/home/node/code/index.js"]

# installs only nodejs from alpine's package manager
# adds a node user and group to run the container as a non-root user
# switches user to node
# makes the work directory as node user, to prevent permission problems
# sets working directory (works like cd)
# copies files from the build step to this dir and transfers ownership to this node user
# CMD runs index.js 
# index.js creates a fastify server that listens on port 8080
# this image runs without npm and node_modules, further storage space is saved

# .dockerignore file is used to ignore stuff just like .gitignore, so we don't copy node_modules, .git and other unnecessary stuff

# Commands to build and run:
# docker build -t multi-stage .
# -t or --tag : name the image
# docker run -it -p 8080:8080 --name my-app --rm --init multi-stage
# --name : names the container
# --publish or -p : maps containers port to host machines port
# --init : container will now respect ur ctrl + c signal to shutdown
# --rm : removes the container when done running
# -it : runs the container in interactive mode, puts you inside the container