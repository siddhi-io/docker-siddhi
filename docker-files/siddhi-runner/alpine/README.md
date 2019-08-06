# Dockerfiles for Siddhi Runner #

This section defines the step-by-step instructions to build [Alpine](https://hub.docker.com/_/alpine/) Linux based Docker image for Siddhi Runner Distribution 5.1.x.

## Prerequisites

* [Docker](https://www.docker.com/get-docker) v17.09.0 or above

## How to build the Siddhi Runner images and run

### Building the Siddhi Runner Base Image
Here we create a base image which contains the default released Siddhi Runner distribution. 

##### 1. Checkout this repository into your local machine using the following Git command.

```
git clone https://github.com/siddhi-io/docker-siddhi.git
```

>The local copy of the `docker-files/siddhi-runner/alpine` directory will be referred to as `DOCKERFILE_HOME` from this point onwards.

##### 2. Build the base Docker image.

- For base, navigate to `<DOCKERFILE_HOME>/base` directory. <br>
  Execute `docker build` command as shown below.
    + `docker build -t siddhiio/siddhi-runner-base-alpine:5.1.x .`

### Building the Siddhi Runner Image

##### 1. Bundling Jars and Bundles
Here we create the Siddhi Runner image bundling the needed extensions and client jars.
       
<DOCKERFILE_HOME>/siddhi-runner/files/ contains two directories (bundles and jars directories) where you can copy the Jars and Bundles you need to bundle into the docker image.
1. Jars directory - Maintained for Jar files which may not have their corresponding OSGi bundle implementation. These Jars will be converted as OSGI bundles and copied to Siddhi Runner docker image during docker build phase. 
2. Bundles directory - Maintained for OSGI bundles which you need to copy to Siddhi Runner docker image directory during docker build phase.
  
##### 2. Build the Runner Docker image
  Execute `docker build` command as shown below. 
    + `docker build -t siddhi-runner-alpine:5.1.x .`
    
### Running Docker image.

    + `docker run -it siddhi-runner-alpine:5.1.x`

## Docker command usage references

* [Docker build command reference](https://docs.docker.com/engine/reference/commandline/build/)
* [Docker run command reference](https://docs.docker.com/engine/reference/run/)
* [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)