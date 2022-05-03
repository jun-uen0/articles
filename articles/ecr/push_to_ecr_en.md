Written with [Cameron Gibson](https://github.com/cgcamcam) 

# Push Docker image to AWS ECR

## Versions
Homebrew 3.4.7
Nginx 1.21.6
Ngrok 3.0.2

## About AWS ECR
AWS ECR is a resitory service like DockerHub.
You can create your own resitory, either public and private.

### How to
1. Prepare Docker image, check it on local
2. Push image to ECR
3. Pull ECR image and check it on local
4. Delete ECR image

# 1. Prepare Docker image, check it on local
Make sure you already have Docker image to push it.
If you're interested in React, take a look at this article: [Dockerizing React App](https://dev.to/jun_uen0/dockerizing-react-app-20gj)
If not, and just want to make a simple image, 
