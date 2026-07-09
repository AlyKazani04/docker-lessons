FROM node:20

USER node

RUN mkdir /home/node/code

WORKDIR /home/node/code

COPY --chown=node:node . .

RUN npm ci

CMD ["node", "index.js"]

# docker build : pulls node:20 from dockerhub
# docker run : runs the container
# switches user to node
# makes the work directory as node user, to prevent permission problems
# sets working directory (works like cd)
# copies files to the workdir and changes ownership to node user
# runs npm ci to install dependencies from package-lock.json
# CMD runs index.js 
# index.js creates a fastify server that listens on port 8080

# .dockerignore file is used to ignore stuff just like .gitignore, so we don't copy node_modules, .git and other unnecessary stuff

# Commands to build and run:
# docker build -t more-complicated-app .
# -t or --tag : name the image
# docker run -it -p 8080:8080 --name my-app --rm --init more-complicated-app
# --name : names the container
# --publish or -p : maps containers port to host machines port
# --init : container will now respect ur ctrl + c signal to shutdown
# --rm : removes the container when done running
# it : runs the container in interactive mode, puts you inside the container