# Run ECS Fargate

## Prepate Docker Image at ECR
If you don't have image at ECR, please check this article and get it.
[Push Docker image to AWS ECR](https://dev.to/jun_uen0/push-docker-image-to-aws-ecr-fb2)
In this article, I use React app image.

## About ECS
AWS Elastic Container Service 
It's a highly scalable and fast container management service.

Terminologies in ECS
- Task / Task Definition: For setting container
- Service: For setting tasks, auto-scalling, VPC, and etc
- Cluster: The cluster of services

## Hands-On Steps
1. Create ECS Cluster
2. Create ECS Task Definition
3. Create ECS Service
4. Confirm ECS Fargate running

# 1. Create ECS Cluster
> ECS Cluster is cluster of services which is EC3 instances. But no one can control the EC2 via SSH access becouse each EC2 instance is hidden.
1. Select "Create Cluster" at ECS console
2. Select "Only net-working (Fargate)"
3. Name cluster
4. Create VPC (optional)
5. "Create"

※ Wait 1 or 2 minutes.

# 2. Create ECS Task Definition
> Task is like a Docker container. In this configure console, you can configure the container. So it's like a docker-compose.yml.

1. Select "Task Definitions" at ECS console
2. Select "Create new Task Definition"
3. Select "Fargate"
4. Name task definition
5. Select "ecsTaskExecution" for task role
6. Select "Linux" for Operating system family
7. Select "0.5GB" for Task memory
8. Select "0.25vCPU" for Task CPU
9. Add container
    - Cqontainer name: Insert name
    - Image: Copy ECR Image URI including tag
    - Port mappings: "3000"
10. Create

# 3 Create ECS Service
> ECS Service is the collection of ECS Tasks and it's related to ALB and AutoScaling Group. ECS Service need ECS Task when created, but it's technically not superordinate of ECS Task becouse you can assign ECS Task to ECS Cluster without Service setting.

- Configure service
1. Select "Cluster" at ECS console
2. Select cluster you created
3. Select "Service" tab
4. Select "Create"
5. Launch type: "Fargate"
6. Task Definition: Select task you created
7. Service name: Insert name
8. Number of tasks: 1
9. "Next step" and skip other items

- Configure network
1. Cluster VPC: choose your VPC for ECS (If you created VPC at "1. Create ECS Cluster", use it )
2. Select Subnets as many as you need
3. Click "Edit" for Security groups
    - Add Inbound rules：custom TCP / Anywhere / port 3000
4. "Next step" and skip other items

- Set Auto Scaling
1. Select "Do not adjust the service’s desired count"
2. "Next step"

⇒ Check all items again, and "Create Service"

# 4. Confirm ECS Fargate running

1. Select "Cluster" at ECS console
2. Select cluster you created
3. Select "Tasks" tab
4. Select task running
5. Copy public IP
6. Access to public IP with `:3000`

Good job.
Plase make sure you deleted the cluster.
It's better to delete any resources in AWS if you don't need to operate it long time or just created for leaning.