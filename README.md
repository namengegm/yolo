# Deploy Containerized Applications To docker hub
## Sample docker images pushed to docker hub

![dockerhub](https://github.com/user-attachments/assets/08c3e8e8-78d1-4cda-a642-759a20b3a25d)
## Choice of the base image on which to build each container.
## Dockerfile directives:
# Build stage
FROM node:16-alpine3.16 as build-stage
# Set the working directory inside the container
WORKDIR /client
# Copy package.json and package-lock.json
COPY package*.json ./
# Install dependencies and clears the npm cache and removes any temporary files
RUN npm install --only=production && \
    npm cache clean --force && \
    rm -rf /tmp/*
# Copy the rest of the application code
COPY . .
# Build the application and  remove development dependencies
RUN npm run build && \
    npm prune --production

# Production stage
FROM node:16-alpine3.16 as production-stage
WORKDIR /client
# Copy only the necessary files from the build stage
COPY --from=build-stage /client/build ./build
COPY --from=build-stage /client/public ./public
COPY --from Build stage
FROM node:16-alpine3.16 as build-stage
# Set the working directory inside the container
WORKDIR /client
# Copy package.json and package-lock.json
COPY package*.json ./
# Install dependencies and clears the npm cache and removes any temporary files
RUN npm install --only=production && \
    npm cache clean --force && \
    rm -rf /tmp/*
# Copy the rest of the application code
COPY . .
# Build the application and  remove development dependencies
RUN npm run build && \
    npm prune --production

# Production stage
FROM node:16-alpine3.16 as production-stage
WORKDIR /client
# Copy only the necessary files from the build stage
COPY --from=build-stage /client/build ./build
COPY --from=build-stage /client/public ./public
COPY --from=build-stage /client/src ./src
COPY --from=build-stage /client/package*.json ./
# Set the environment variable for the app
ENV NODE_ENV=production
# Expose the port used by the app
EXPOSE 3000

# Prune the node_modules directory to remove development dependencies and clears the npm cache and removes any temporary files


# Start the application
CMD ["npm", "start"]=build-stage /client/src ./src
COPY --from=build-stage /client/package*.json ./

# Set the environment variable for the app
ENV NODE_ENV=production

# Expose the port used by the app
EXPOSE 3000

# Prune the node_modules directory to remove development dependencies and clears the npm cache and removes any temporary file

# Start the application
CMD ["npm", "start"]

## Docker-compose Networking 
Created and linked a container to same network in the docker yml file

## Docker-compose volume definition and usage
Created and attached a volume to containers in the docker yml file. This is to help persit the data even after the container is not running

## Git workflow 
 - create docker file to help create images
 - create docker file yml
 - create docker image
 - Run container from the docker image created
 - Push the image to docker hub for remote access and back up.
## Successful running of the applications.
Permission issues check resolution https://stackoverflow.com/questions/48957195/how-to-fix-docker-got-permission-denied-issue

### Good practices 
- create images with a version name
- Run containers with tag -rm to remove it after it is stopped
- Ensure containers have version tags, volume attached and are run from the stable images
