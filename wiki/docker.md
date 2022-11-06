# Docker
Docker packages software so that it can run on any hardware.

* `docker ps` - list running docker processes 
 
## Dockerfile
Every instruction creates a cached layer
* `FROM` - Specifies a base image (ex. ubuntu, node)
* `WORKDIR` - Sets working directory (kind of like `cd`)
* `COPY` - Copy file(s) from local into container
* `RUN` - Runs command (shell form)
* `ENV` - Set environment variables
* `EXPOSE` - Define the port for the container to listen on at runtime
* `CMD` - Tells container how to run the application (can only have 1 per docker container) (defined in exec form, ie an array of strings)

## Docker build
Build a docker image:
`docker build -t username/imagename:version.number /path/to/Dockerfile`

You can push / pull docker images to a docker image registry like dockerhub with `docker push` / `docker pull`

## Docker run
`docker run {image tag / hash}`

Port Forwarding
`docker run -p {local port}:{container port} {image tag / hash}`

## Volumes
Share data between containers
`docker volume create ...`

## Debugging
`docker exec` puts you in a cli inside the container
1 process per container

## Docker compose
* Compose is a tool for running multi-container Docker applications
* `docker-compose.yml` configures your applications services based on docker images.
* `docker-compose up` then starts your application
    * `-d` starts it in the background
* `docker-compose down` tears down the application
* `docker-compose logs` lets you read the logs from the application(s) you've started

