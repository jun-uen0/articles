Written with [Cameron Gibson](https://github.com/cgcamcam) 

# Pull Nginx image and run the container

## Versions
OS: MacOS (intel chip)
Docker version: 20.10.12  

## Official image of Nginx
Nginx distribute its official Docker image on Docker Hub.
https://hub.docker.com/_/nginx

## How to
1. Pull Nginx Docker image
2. Run the container

## 1. Pull Nginx Docker image
① Pull the latest of Nginx Docker image
```shell
docker pull nginx
```
② Confirm you successfully pulled the image
```
docker images
```

## 2. Run the container
① Run the container
Listen Port: 3000, Forward to: 80
```shell
docker run -p 3000:80 nginx
```
② Confirm you successfully run the container
Access to http://localhost:3000/

## Thank you
I hope this helps.
Thank you for reading.