
Docker File: The list of instruction on how to build your docker image

Docker Image: The compiled code that you can then run to create a docker container

Docker Container: An environment / mini computer than can have dependencies and OS's installed into it to be able to run software in a incredibly modular way

Docker Hub: The website / database that can store your docker images that you can pull/push to

Types of Instructions:

```
FROM <image> - Defines base image to start from like ubuntu
RUN <command> - Runs shell commands inside the image and saves as a new image layer
WORKDIR <directory> - Sets the directory for other commands
COPY <src> <dest> - copies files to a new folder
CMD <command> lets you devide commands to run once the container is running
```

```Dockerfile
# syntax=docker/dockerfile:1
FROM ubuntu:22.04

# install app dependencies
RUN apt-get update && apt-get install -y python3 python3-pip
RUN pip install flask==3.0.*

# install app
COPY hello.py /

# final configuration
ENV FLASK_APP=hello
EXPOSE 8000
CMD ["flask", "run", "--host", "0.0.0.0", "--port", "8000"]
```

Docker Caching: Docker caches each later of the image so you don't have to rebuild everything every time