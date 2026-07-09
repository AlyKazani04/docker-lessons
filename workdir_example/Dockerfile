FROM node:20

USER node

WORKDIR /home/node/code

COPY --chown=node:node index.js .

CMD ["node", "index.js"]

# docker build : pulls node:20 from dockerhub
# docker run : runs the container
# switches user to node
# sets working directory (works like cd)
# copies files to the workdir and changes ownership to node user
# CMD runs index.js 
# index.js creates a server that listens on port 3000

# Commands to build and run:
# docker build -t my-node-app .
# -t or --tag : name the image
# docker run --init --publish 3000:3000 --rm my-node-app
# --publish or -p : maps containers port to host machines port
# --init : container will now respect ur ctrl + c signal to shutdown
# --rm : removes the container when done running