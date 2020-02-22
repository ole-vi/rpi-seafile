# rpi-seafile

## Basic information

I refer a Dockerimage: https://github.com/yuriteixeira/rpi-seafile

There are two major versions in Seafile.
Old version: version 6.*.*
New version: version 7.*.*

Old version works as just one Docker image.
New version is designed as Docker services; Seafile service works with three Docker images. 

The Dockerfile which to I refer uses old version. 

## How to make iamge

1 Build base image
The base image of Dockerfile is in python directory
Name the base image as "rpi-python:stretch

1 Build Seafile image
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
1 server name 
A. anything
1 ip address or domain name
A. your onion address
1 volume path
A. just push Enter
1 TCP port for seafile server
A. Just push Enter

After that, you are asked to several questions, but all of them are confirmation.
Therefore, just push Enter

After finishing the configuration, execute `./seafile.sh start`

Adter that, execute `./seahub.sh start 8000`

Then you are asked two questions
1 Admin email address
1 Admin password

They are used to enter the seafile from Tor browser, so need to note them somewhere or memorize them.








