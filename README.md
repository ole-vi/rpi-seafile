# Seafile for raspberry pi

## Basic information

I refer a Dockerimage: https://github.com/yuriteixeira/rpi-seafile

Fortunately, this Docker image can be used without any modification.

However, the very base image of this seafile image is Rasbian wheezy, so we cannot change the Dockerfile of the image at all.
Therefore. I built the base emage: pythyon-rpi from resin/rasbian:stretch

This Dockerfile can download the latest seafile server images for Raspberry Pi.

## Deploy Service

```
docker run -e SEAFILE_NAME=Seaflail 
-e SEAFILE_ADDRESS=[ip address/onion address/domain name] 
-e SEAFILE_ADMIN=[email address] 
-e SEAFILE_ADMIN_PW=[password] 
-v /home/data/seafile:/seafile 
-p 8000:8000 -p 8082:8082 hirotochigi/seafile-rpi
```

## How to make image

1. Build base image
The base image of Dockerfile is in python directory
Name the base image as "rpi-python:stretch

1. Build Seafile image
The Seafile image of Dockerfile is in seafile directory.

After building the seafile image out of the Dockerfile, spawn the container following command

```
docker run -e SEAFILE_NAME=Seaflail 
-e SEAFILE_ADDRESS=[your onion address] 
-e SEAFILE_ADMIN=[email address] 
-e SEAFILE_ADMIN_PW=[password] 
-v /home/data/seafile:/seafile 
-p 8000:8000 -p 8082:8082 [image name]
```


