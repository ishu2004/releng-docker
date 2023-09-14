# Robot Framework Docker Container

This Dockerfile facilitates the creation of a Docker image that comprises a comprehensive Robot Framework environment built on CentOS 8. The image is equipped with Python 3.10.2, Java 17, and all the necessary dependencies essential for executing Robot Framework tests efficiently.

## Prerequisites

Before you proceed with building and running this Docker image, ensure that you have Docker properly installed on your system.

## How to Use

To seamlessly build the Docker image and execute Robot Framework tests within a container, adhere to the following steps:

Step 1: Clone the Repository

Begin by cloning this repository to your local machine:

```
git clone https://github.com/askb/releng-docker
cd robot-framework-docker
```

Step 2: Build the Docker Image
Execute the following command to build the Docker image:

```
docker build -t robot-framework:latest .
```

Step 3: Run a Docker Container

Once the image has been successfully constructed, launch a Docker container from it. You have the flexibility to replace 'my-robot-container' with a name of your choice:

```
docker run -it --network=host --name my-robot-container robot-framework:latest bash -c "tail -f /dev/null"
```

Ensure that opendaylight and Robot containers are on the same Docker network.

You can now access the container using

`$ docker exec -it my-robot-container bash `

Step 4: Run the OpenDaylight container on the same network.

```
docker run -d --name opendaylight --network=host opendaylight-image --env FEATURES=odl-restconf,odl-netconf-topology
```

Step 5: Clone the integration-test repository

```
docker exec robot-container bash -c 'git clone https://github.com/opendaylight/integration-test.git"
```

Step 6: Run single integration test

```
    docker exec robot-container bash -c '
    robot -L debug --variable KARAF_HOME:/home/user/workspace/netconf/karaf/target/assembly/bin --variable USER_HOME:/home/jenkins --variable DEFAULT_LINUX_PROMPT:\$ --variable ODL_SYSTEM_IP:127.0.0.1 --variable ODL_SYSTEM_1_IP:127.0.0.1 --variable RESTCONFPORT:8181 --variable IS_KARAF_APPL:True ./test.robot'
```

For Example

```
          docker exec robot bash -c 'git clone https://github.com/opendaylight/integration-test.git &&       
            cd integration-test/csit/suites/daexim &&
          robot -L debug --variable USER_HOME:/root \
            --variable WORKSPACE:/home/youruser \
            -v BUNDLEFOLDER:karaf-0.18.1 \
            -v ODL_STREAM:argon \
            --variable DEFAULT_LINUX_PROMPT:\$ \
            --variable ODL_SYSTEM_USER:youruser \
            --variable ODL_SYSTEM_IP:localhost \
            --variable ODL_SYSTEM_1_IP:localhost \
            -v IS_KARAF_APPL:True \
                  ./010-special-export.robot 020-import-basic.robot 030-export-basic.robot 040-export-inclusions.robot '
```
