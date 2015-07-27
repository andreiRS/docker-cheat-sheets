# docker cheat sheets

## Examples Commands

```
# show all images
docker images

# show all containers
docker ps

# remove all containers
docker rm $(docker ps -a -q)

# remove all images 
docker rmi $(docker images -q)

# builds an image with the #IMAGE_NAME#
docker build -t #IMAGE_NAME# .

# connect to container via bash terminal
docker run -i -t #IMAGE_NAME# /bin/bash

# runs the image as daemon with port mapping
docker run -d -p 8888:8888 #IMAGE_NAME#

# runs an image with volumes mounted from host
docker run -d -p 8888:8888 -v /Users/andrei/Projects/start-go-project/:/apps/html go-image

# connect to container
docker run -i -t -p 8888:8888 -v /Users/andrei/Projects/start-go-project/:/apps/html go-image /bin/bash
```

## Examples Dockerfile
```
FROM ubuntu:14.04

RUN apt-get update
RUN apt-get install -y git curl nano golang nginx

RUN curl https://raw.githubusercontent.com/andreiRS/dotfiles/master/.bashrc > /root/.bashrc
RUN mkdir /apps


ADD . /apps/html

RUN mv /etc/nginx/nginx.conf /etc/nginx/nginx.conf.original
RUN mv /apps/html/nginx.conf /etc/nginx/nginx.conf

WORKDIR /apps/html

EXPOSE 8888
CMD ["nginx"]
```
