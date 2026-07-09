FROM node:20-alpine
# Alpine is a smaller distro, so saves up on build time and image size.
# node:20-alpine => 133MB while node:20 => about 1.0GB
# Its a good idea to user smaller distros for production images.
# For Dev, its still better to use the full distro, as it has more tools and utilities for debugging and development.

USER node

RUN mkdir /home/node/code

WORKDIR /home/node/code

COPY --chown=node:node package-lock.json package.json ./

RUN npm ci

COPY --chown=node:node . .

CMD ["node", "index.js"]

# docker build : pulls node:20 from dockerhub
# docker run : runs the container
# switches user to node
# makes the work directory as node user, to prevent permission problems
# sets working directory (works like cd)
# The first COPY pulls just the package.json and the package-lock.json which is just enough to do the npm ci.
#   Now if you make changes you avoid doing a full npm install. 
#   This is useful and recommended for any dependency installation: apt-get, pip, cargo etc. as well as any long-running command.
# runs npm ci to install dependencies from package-lock.json
# copies rest of the files to the workdir and changes ownership to node user
# CMD runs index.js 
# index.js creates a fastify server that listens on port 8080

# .dockerignore file is used to ignore stuff just like .gitignore, so we don't copy node_modules, .git and other unnecessary stuff

# Commands to build and run:
# docker build -t layers .
# -t or --tag : name the image
# docker run -it -p 8080:8080 --name my-app --rm --init layers
# --name : names the container
# --publish or -p : maps containers port to host machines port
# --init : container will now respect ur ctrl + c signal to shutdown
# --rm : removes the container when done running
# -it : runs the container in interactive mode, puts you inside the container