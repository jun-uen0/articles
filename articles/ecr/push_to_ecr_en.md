Written with [Cameron Gibson](https://github.com/cgcamcam) 

# Push Docker image to AWS ECR

# Versions
Homebrew 3.4.7
Nginx 1.21.6
Ngrok 3.0.2
AWS CLI 2.5.8

# About AWS ECR
AWS ECR is a repository service like DockerHub.
You can create your own repository, either public or private.

# How to
1. Prepare Docker image, check it on local environment
2. Push the image to ECR
3. Pull ECR image and check it on local environment
4. Delete ECR image

# 1. Prepare Docker image, check it on local enviroment
Make sure you already have a Docker image to push it.
If you're interested in React, take a look at this article: [Dockerizing React App](https://dev.to/jun_uen0/dockerizing-react-app-20gj).
If you don't have any images and just want to make a simple image, check it out: [Pull Nginx image and run the container](https://dev.to/jun_uen0/pull-nginx-image-and-run-the-container-4de8)

# 2. Push to AWS ECR
① Create your public image repository at [ECR console](https://console.aws.amazon.com/ecr/repositories)

② Click "View push command"

③ Copy & run 1st command using AWS CLI, and login to AWS
```shell
aws ecr-public get-login-password --region <your region> | docker login --username AWS --password-stdin public.ecr.aws/~~~

Login Succeeded
```

※ Skip 2nd command, we already have the image on local environment.

④ Copy & run the 3rd command, and tag your image to push to ECR
```shell
docker tag <your local image name>:latest public.ecr.aws/~~~~~/<your ECR repository name>:latest
```

⑤ Copy & run the 4th command, and push the image to ECR
```shell
$ docker push public.ecr.aws/~~~~~/<your ECR repository name>:latest

# output
The push refers to repository [public.ecr.aws//~~~~~/<your ECR repository name>]
6532d1bd92d7: Pushing [========================================>          ]    181MB/223.4MB
1bfe2f2c209c: Pushing [==============================>                    ]  156.5MB/259.2MB
5bc57cb39f11: Pushed 
1f63745992bb: Pushed 
fea31d3e0c85: Pushed 
0fc8a3e8b32a: Pushed 
99307ceff565: Pushed 
5cc685c4cd61: Pushed 
6fd97e423126: Pushed 
ca58f1c44290: Pushing [==================>                                ]  188.3MB/510.5MB
957a6eed8d1f: Pushing [==========================================>        ]  123.8MB/145.5MB
85fe00380881: Pushing [==================================================>]  17.87MB
5d253e59e523: Waiting 
b9fd5db9c9a6: Waiting 
```
⑥ Go back to ECR console
(add #7) Click your repository name and confirm you successfully pushed the image to ECR

# 3. Pull ECR image and check it on local environment
① Delete the image you tagged
```shell
docker rmi public.ecr.aws/~~~~~/<your ECR repository name>:latest
```
② Copy the URI of the image you pushed at ECR console and pull the image.
The image URI must be exactly the same, but it's better to know where you can check the image URI.

```shell
$ docker pull <URI you copied at ECR console>

# output
latest: Pulling from ~~~~~
Digest: sha256:~~~~~~~~~~~~~~~~~~~~
Status: Downloaded newer image for <URI you copied at ECR console>
<URI you copied at ECR console>
```

③ Run the container you pulled from ECR
```shell
docker run -p 3001:3000 <URI you copied at ECR console>
```
③ Confirm you successfully ran the container
Access to http://localhost:3001

# Thank you
I hope this helps.
Thank you for reading.