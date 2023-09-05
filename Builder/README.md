# OpenDaylight Builder Docker Image

The provided Dockerfile is intended for building OpenDaylight projects. It sets up an environment with the necessary dependencies, including Java and Maven, to build OpenDaylight projects from source code. You can use this Docker image to build the OpenDaylight projects

## Building the Docker Image

You can build the Docker image for the desired base system (Ubuntu or CentOS) using the following commands:

### Ubuntu Base Builder Image

```
$ docker build -t builder_image_name ./Ubuntu/
```
### CentOS Base Builder Image
```
$ docker build -t builder_image_name .\Centos\ 
```
Replace Builder_Image_Name with your preferred image name.

### Using the Builder Image for MVN Builds 
Once you've built the Builder image, follow these steps to perform MVN builds within a Docker container:

1) Launch a Docker container:
```
$ docker run --name my-builder-container builder_image_name bash -c "tail -f /dev/null"

```
2) Access the Docker container:
```
$ docker exec -it my-builder-container bash
```
3) Inside the Docker container, clone the OpenDaylight repository you want to build:
```
$ git clone https://git.opendaylight.org/gerrit/integration/distribution
$ cd distribution
```
4) Run the Maven (MVN) build:
```
mvn clean install
```
This will initiate the build process for the OpenDaylight project. Make sure you replace the example Git URL (https://git.opendaylight.org/gerrit/integration/distribution) with the URL of the specific OpenDaylight repository you intend to build.
By following these steps, you can use the provided Docker image to build OpenDaylight projects with a consistent development environment.
