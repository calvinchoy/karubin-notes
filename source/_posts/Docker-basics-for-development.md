---
title: Docker basics for development
tags:
	- devops
	- docker
	- development
	- tooling
categories:
	- devops
	- tooling
date: 2020-09-20 16:49:42
---

An overview of some core commands for running docker containers for development purposes. Installation and on why use docker will not be explained here, refer to the official docker documentation for more that. These are just some notes that I made while learning the basics of docker for local development usage.

<!-- more -->

## Concept

Use docker container virtualization to spin up a development environment. For example: nginx server and a database. The container will expose ports to connect to from your local (host) machine to the container (guest machine).

Containers can be ran from command line, or from a `docker-compose.yml` file. The later one is recommended as it will save you from retyping the cli commands everytime and also a best practice in term of versioning configuration management. Below are some basic concepts you need to understand while using containers for local development:

- Run each service as a separate container
- Run containers as daemon in background (`-d`) and access it using the exposed port
- Data can be managed using volumes, this allows you to persist your data when a container is destroyed
- Network among containers are set by default by docker, don't use IP address use the container name which will be aliased to vpn created by docker when multiple containers are ran
- Dockerfile - is like a recipe to create your own image file which can then be used to spin containers from
- `docker-compose.yml` - orchestrate executing your containers by means of configuration file instead of the docker cli

## Running new container

```bash
docker container run -it -d -p 8080:80 --name web nginx
```

When this command is ran the following is happening

1. Docker checks if it can find an image called nginx. If not it will download the latest from repository
2. Docker wil run a container using the supplied image
3. `-d` means it will detach after running
4. `-it` mean it will create a tty terminal for it
5. `--name` top give an alias name
6. `-p` stands for publish and will configure NAT rules `host:container` to open ports for communication
7. You can now access your server on port 8080 on your computer (host) to connect to port 80 from the container (nginx default port)

## Inspecting container processes

```bash
# list running containers
docker container ls
# check container run logs while running, using -f flag
docker container logs -f <container>
# process list in one container
docker container top <container>
# details of one container config
docker container inspect <container>
# performance for all containers
docker container stats
```

## Getting shell access to a container

```bash
# When running a new container
docker container run -it ....
# When restarting a container
docker container start -ai <container>
# Attach to running container
docker container exec -it <container> <command i.e. bash>
```

## Docker Networking

Docker use defaults that most of the time just works for networking. When a container is created by docker it will create a default virtual private network. By specifying the -p option it will configure a NAT rule between the `host_port:container_port`.

All containers inside the same vpn can see each other using their virtual IP address. We can create multiple vpn can attach/detach container to one or more networks[.](http://networks.By) By default, DNS daemon is built-in the docker networks and the container name is used as host names that resolves to their corresponding ip address → don't rely on ip addresses

```bash
# Check open ports
docker container port <container>

# Check ip address
docker container inspect --format '{{.NetworkSettings.IPAddress}}' <container>
```

### Network CLI-Management

```bash
docker network ls
docker network create
docker network inspect
docker network connect
docker network disconnect
```

## Container lifecycle and data management

Containers are used to be immutable and ephemeral, that is it should be disposable and we can recreate them anytime from an image when that is needed or when we want to deploy a new updates version of the container. What important is the separate of concern regarding the data that is stored and mutated by the application running inside the container.

Docker offers two way of persistent data mangement:

1. volume mounts — where the persistent data is stored to a location outside of the container
2. bind mounts — link a container path to a path on the hosts, like symlinking

### Data volumes

Some images uses volumes to maintain persistent data. That data is not automatically deleted when the container is stopped or removed. You will need an extra step to remove the data from the volume mount location. It is recommended to specify a named path when using volume data mounting.

```bash
# inspect image to check for default volume mount
docker image inspect <image name>

# aliasing a volume mount
docker container run -it -d -p -v volumeName:/path/to/volume --name web mysql

# listing persistent volumes on host
docker volume ls
```

### Bind mounting

This is like symlink of directories but instead you are making a link between a host directory to directory inside the container. This is often useful for development. While a data volume can be specified in a dockerfile, bind mounting cannot and needs to be specified during container run.

```bash
# to map to host current directory you can use $(pwd)
docker container run -it -d -p 8080:80 -v /path/on/host:/path/on/container --name web nginx
```

## Docker file

> A Dockerfile is like a recipe for creating an image which can then be used to run a container from it

The `Dockerfile` will be used to specify and provision your image when it is ran as container. For example, things to include in dockerfiles:

- FROM, base image to extend from
- ENV, environment variables
- RUN, commands to run during setup in container
- EXPOSE, export ports
- CMD, command to execute after container is up

Note: When creating docker file make sure that things that change the less are at the top, and the most at the bottom. This has to do that each step in the `Dockerfile` is hashed and unless there are changes it does not have to rebuild.

### Example

```jsx
//use default nginx image as basis to extend
FROM nginx:latesst

//change directory inside container
WORKDIR /usr/share/nginx/html

//copy file from host to container
COPY index.html index.html
```

### Building an image

```jsx
docker iamge build -t <name> <path/to/dockerfile/target>
```

- `-t`, tagging image with a name

## Docker compose

Instead of running docker cli commands manually to manage your containers you can use a `.yml` file to specify it in a template format. This makes it easy for version management and distribution across teams. Docker compose is mainly used for local development.d

### Structure of a basic docker compose file

```yaml
version: '3.0'

services: #list the containers you want to run
	servicename1:
		image:
		build:
			context:
			dockerfile:
		command:
		ports:
		environment:
        volumes:

	servicename2:
		image:
		command:
		ports:
		environment:
		volumes:

volumes:

networks:

```

### Example

Below will run two containers. One for drupal and one for postgres. The configuration details can be found on docker hub image file documentation or you can use `docker image inspect` after the image is pulled in using `docker pull`.

```jsx
version: '3'

services:
	drupal:
		image: druppal
		ports:
			"8080":"80"
		volumes:
			...
	postgres:
		image: postgres
		environment:
			POSTGRES_PASSWORD=somepassword

volumes:
		...
```
