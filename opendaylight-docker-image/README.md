# Opendaylight Docker Image

This Dockerfile creates an image that contains the Opendaylight Karaf distribution and an SSH server. The image can be used to run Opendaylight as a container and access it via SSH.

## Prerequisites

- Docker installed on your machine
- A base image of either Ubuntu or CentOS

## Build the Image

By default, the Dockerfile uses Ubuntu as the base image. To build the image with CentOS as the base OS and specify the Karaf version as build arguments, run the following command:

```bash
docker build --build-arg BASE_IMAGE=centos --build-arg KARAF_VERSION=0.18.1 -t opendaylight:0.18.1 .
```

This will create an image named opendaylight:0.18.1 with Centos as the base OS and Karaf 0.18.1 as the Opendaylight distribution.

## Run the container
To run the container, run the following command:
```bash
 docker run -p 8181:8181 -p 8101:8101 -p 2222:22  opendaylight:0.18.1
```
### Environment Variables
You can customize the behavior of the OpenDaylight container using environment variables:

`FEATURES`: Specifies the Karaf features to be installed. For example, if you want to install additional features, set the FEATURES environment variable when running the container. For example:

```bash
    docker run -d -p 8181:8181 -p 8101:8101 -p 2222:22 --name opendaylight --env FEATURES=odl-restconf,odl-netconf-topology  opendaylight:0.18.1
```
### Access the container
To access the container ,
```bash
docker exec opendaylight -it  bash
```
