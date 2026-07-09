FROM node:20

COPY index.js index.js

CMD ["node", "index.js"]

# docker build : pulls node:20 from dockerhub
# docker run : runs the container
# CMD runs index.js 
# index.js creates a server that listens on port 3000

# Commands to build and run:
# docker build -t my-node-app .
# -t or --tag : name the image
# docker run --init --publish 3000:3000 --rm my-node-app
# --publish or -p : maps containers port to host machines port
# --init : container will now respect ur ctrl + c signal to shutdown
# --rm : removes the container when done running