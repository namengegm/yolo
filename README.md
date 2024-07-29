# Pushing Docker image to docker hub
## Sample docker images pushed to docker hub
### My docker hub link:
https://hub.docker.com/
![dockerhub3](https://github.com/user-attachments/assets/4b065e6c-97c6-4b1f-9c25-89558ab76f3a)
## Choice of the base image on which to build each container.
## Dockerfile directives:
 - Build stage
FROM node:16-alpine3.16 as build-stage
 - Set the working directory inside the container
WORKDIR /client
 - Copy package.json and package-lock.json
COPY package*.json ./
 - nstall dependencies and clears the npm cache and removes any temporary files
RUN npm install 
    npm cache clean --force && \
    rm -rf /tmp/*
 - Copy the rest of the application code
COPY . .
 - Build the application 
RUN npm run build 
 
 - Start the application
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
- Create images with a version tags.
- Run containers with tag -rm to remove it after it is stopped.
- Run container with a flag -d in detached mode to allow user interact with cmd
- Ensure containers have version tags, volume attached and are run from the stable images.
