# AWS

## Learn List
* VPC

## RDS


## Deploy a docker container to EC2
Adapted from https://levelup.gitconnected.com/deploy-a-dockerized-fastapi-application-to-aws-cc757830ba1b

1. Create the docker app
* Set up a virtual env with fastapi, uvicorn, etc..
* Freeze the pip requirements
* Write the FastAPI python app
* Create the Dockerfile
* Build the docker image:
    * `docker build -t fastapi-demo .`
* Run it to verify:
    * `docker run -dp <host_port:docker_port> <name_of_image>`

2. EC2 Setup
* Launch an EC2 instance
* Create a keypair and save the .pem file for ssh usage
```
chmod 400 fastapi-deploy-demo.pem # Substitute with your key
ssh -i "fastapi-deploy-demo.pem" ec2-user@<your-details-here>.compute-1.amazonaws.com
```
* Install and start docker 
```
# Update the installed packages and package cache on your instance.
sudo yum update -y
# Install the most recent Docker Community Edition package.sudo 
amazon-linux-extras install docker
# Start the Docker service.
sudo service docker start
# Add the ec2-user to the docker group so you can execute Docker #commands without using sudo.
sudo usermod -a -G docker ec2-user
```

3. ECR setup 
* Create an ECR repository
* On your dev host authenticate your docker client via the AWS CLI (follow instructions for push commands in ecr)
* Push your image to ECR:
```
# Navigate to the project directory first and type the following:
docker build -t fastapi-deploy-demo .
# Tag the image
docker tag fastapi-deploy-demo:latest <YOUR ID>.dkr.ecr.us-east-1.amazonaws.com/fastapi-deploy-demo:latest
# PUSH
docker push <YOUR ID>.dkr.ecr.us-east-1.amazonaws.com/fastapi-deploy-demo:latest
```

4. EC2 pull and run image
* ssh into ec2 instance
* run `aws configure`
* authenticate docker client as before
```
docker pull <IMAGE_URI> # that you grab from ecr repository
docker images # check that image is there 
docker run -dp 80:8000 <NAME_OF_IMAGE>
```
* Edit the inbound rules in EC2 AWS UI console to allow all inbound traffic
* Go to the IPV4 address of the EC2 instance

