### Python Docker
This is a sample flask app bundled up with Docker

#### Content
[Installation and Setup](#installation-and-setup)
[Prerequisites](#prerequisites)
[Local Development](#local-development)
[Build the image](#build-the-image)
[Tagging the image](#tagging-the-image)
[Running the image](#run-the-image)
[Working with the container](#working-with-containers)
[Github Actions](#github-actions)

***
# Installation and Setup
![mac](https://img.shields.io/badge/mac%20os-000000?style=for-the-badge&logo=apple&logoColor=white)
![linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)

## Prerequisites
![docker](https://img.shields.io/badge/Docker-2CA5E0?style=for-the-badge&logo=docker&logoColor=white)
![python](https://img.shields.io/badge/Python-FFD43B?style=for-the-badge&logo=python&logoColor=blue)
![git](https://img.shields.io/badge/GIT-E44C30?style=for-the-badge&logo=git&logoColor=white)

#### Local Development
Run the following in the terminal to setup virtual environment
```shell
python3 -m venv venv
source venv/bin/activate

# install dependencies
python3 -m pip3 install -r requirements.txt
```

#### Build the Image
```shell
docker build -t python-docker .
```
> Docker builds as latest

You can verify that by typing the following command:
```shell
docker images

# the output is similar to this
(venv) Ξ PycharmProjects/python-docker → docker images
REPOSITORY      TAG            IMAGE ID       CREATED         SIZE
python-docker   latest         23847fed8b84   4 minutes ago   121MB
```

### Tagging the image
```shell
docker tag python-docker:latest python-docker:v1.0.0

# docker tag creates a new image, confirm by typing
docker images

# the output is similar to this
(venv) Ξ PycharmProjects/python-docker → docker images
REPOSITORY      TAG            IMAGE ID       CREATED          SIZE
python-docker   latest         23847fed8b84   16 minutes ago   121MB
python-docker   v1.0.0         23847fed8b84   16 minutes ago   121MB
```

### Run the image
Run with `-p` to publish on a port and `-d` in detach mode. Use `docker logs flask-app` to check logs or with `-f` flag to stream the log live.
```shell
docker run -p 8000:5000 python-docker
# Flask runs on  http://127.0.0.1:8000 whiles running on port 5000 inside the 
# container

# output on the cli is similar to this
(venv) Ξ PycharmProjects/python-docker → docker run --name flask-app -p 8000:5000 python-docker
 * Debug mode: off
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on all addresses (0.0.0.0)
 * Running on http://127.0.0.1:5000
 * Running on http://172.17.0.2:5000
Press CTRL+C to quit
172.17.0.1 - - [21/Apr/2023 09:27:24] "GET / HTTP/1.1" 200 -
172.17.0.1 - - [21/Apr/2023 09:27:24] "GET / HTTP/1.1" 200 -
172.17.0.1 - - [21/Apr/2023 09:27:24] "GET /favicon.ico HTTP/1.1" 404 
```

### Working with containers
```shell
# show running containers. or with -a to show stopped and running containers
docker ps

# show logs
docker logs flask-app

# stop a container. use container name or id
docker stop flask-app

# restart a container
docker restart flask-app

# remove a container
docker rm flask-app
```

> NB: The docker-compose.yml file is just for reference.
> We are not using database in the app just yet :)

```shell
# this will build and run the container
docker compose -f docker-compose-dev.yml up --build
```

### Github Actions
Environment variables have to be added to Github Secrets for the flow to work :)
Generate `DOCKERHUB_USERNAME` and `DOCKERHUB_TOKEN` in secrets section and pick the values from 
Docker website account section.
