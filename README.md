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
docker run -it -e SEAFILE_NAME=Seaflail -e SEAFILE_ADDRESS=[your onion address] -e SEAFILE_ADMIN=[email address] -e SEAFILE_ADMIN_PW=[password] -v /home/data/seafile:/seafile -p 8000:8000 -p 8082:8082 [image name]
```

In this time, -e flag do nothig because you do not execute any entrypoint.sh
If the entrypoint.sh works, you can use them.

After spawning the seafile container, go to `/opt/haiwen/seafile-server-6.3.4`

Then, execute `setup-seafile.sh`

You are asked the following
1. Q. server name 

A. anything
1. Q. ip address or domain name

A. your onion address
1. Q. volume path

A. just push Enter
1. Q. TCP port for seafile server

A. Just push Enter

After that, you are asked to several questions, but all of them are confirmation.
Therefore, just push Enter

After finishing the configuration, execute `./seafile.sh start`

Adter that, execute `./seahub.sh start 8000`

Then you are asked two questions
1 Admin email address
1 Admin password

They are used to enter the seafile from Tor browser, so need to note them somewhere or memorize them.

## Problem of entrypoint.sh

```
[02/21/20 05:16:55] ../common/ccnet-db.c(142): 
Error exec query CREATE UNIQUE INDEX IF NOT EXISTS reference_id_index on EmailUser (reference_id): 
sqlite3_exec failed: table EmailUser has no column named reference_id.
[02/21/20 05:16:55] user-mgr.c(769): Failed to create user db tables.
failed to run "ccnet-server -t"
```

In my case, sqllite does not start correctly.
I think that we need to analyze what `setup-seafile.sh` is doing in the configuration process to make the proper entrypoint.sh

