# Dockerizing React App

### Versions
Node version: 16.13.0  
Docker version: 20.10.12   

### Link
GitHub Repo   
https://github.com/jun-uen0/react-dockerfile

Here’s How to Dockerize React App  
https://www.bacancytechnology.com/blog/dockerize-react-app


### Table of Contents
1. Create React app
2. Create Dockerfile, image and run the container

## 1. Create React app
① Create React App following [official tutorial](https://reactjs.org/docs/create-a-new-react-app.html)  
② Run command below
```shell
npx create-react-app <app name> # which is going to be the folder name
cd <app name>
npm start
```
③ Access to http://localhost:3000   
Confirm you can see React app welcome page

④ Stop Running by Ctrl + C

## 2. Create Dockerfile, image and run the container
① Create `Dockerfile` in root directory  
And copy the code below 
```yml
# Dockerfile
FROM node:16
WORKDIR /reactapp
ENV PATH /reactapp/node_modules/.bin:$PATH
COPY package.json ./
COPY package-lock.json ./
RUN npm i
COPY . ./
CMD ["npm", "start"]
```

② Build image
```
docker build -t <image name> . 
```
③ Run container
```shell
docker run \
    -it \
    --rm \
    -v ${PWD}:/reactapp \
    -v /reactapp/node_modules \
    -p 3000:3000 \
    -e CHOKIDAR_USEPOLLING=true \
    <image name>:latest
```
④ Access to http://localhost:3000  
Confirm you can see React app welcome page