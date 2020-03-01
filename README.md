# Seafile-rpi

## Basic information

I refer a Dockerimage: https://github.com/yuriteixeira/rpi-seafile

Fortunately, this Docker image can be used without any modification.

However, the very base image of this seafile image is Rasbian wheezy, so we cannot change the Dockerfile of the image at all.
Therefore. I built the base emage: pytyon-rpi from resin/rasbian:stretch

Then, I built the Seafile-rpi image from the python-rpi.


There are two major versions in Seafile.

Old version: version 6.*.*

New version: version 7.*.*


Old version works as just one Docker image.

New version is designed as Docker services; Seafile service works with three Docker images.

Please look at [https://download.seafile.com/published/seafile-manual/deploy/deploy_with_docker.md#user-content-Download] to get more detail information.


The Dockerfile which to I refer uses old version. 

## How to make image

1. Build base image
The base image of Dockerfile is in python directory
Name the base image as "rpi-python:stretch

1. Build Seafile image
The Seafile image of Dockerfile is in seafile directory
entrypoint.sh is disabled because it does not work.

After building the seafile image out of the Dockerfile, spawn the container following command

```
docker run -e SEAFILE_NAME=Seaflail 
-e SEAFILE_ADDRESS=[your onion address] 
-e SEAFILE_ADMIN=[email address] 
-e SEAFILE_ADMIN_PW=[password] 
-v /home/data/seafile:/seafile 
-p 8000:8000 -p 8082:8082 [image name]
```


