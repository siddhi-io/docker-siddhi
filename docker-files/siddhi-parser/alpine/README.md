# Dockerfiles for Siddhi Parser #

This section defines the step-by-step instructions to build [Ubuntu](https://hub.docker.com/_/ubuntu/) Linux based Docker image for Siddhi Parser Service 0.1.0.

## Prerequisites

* [Docker](https://www.docker.com/get-docker) v17.09.0 or above

## How to build the Siddhi Parser images and run

##### 1. Checkout this repository into your local machine using the following Git command.

```
git clone https://github.com/siddhi-io/docker-siddhi.git
```

>The local copy of the `dockerfiles/siddhi-parser/alpine` directory will be referred to as `DOCKERFILE_HOME` from this point onwards.

##### 2.Copy Siddhi Parser JAR and extension JARS to `<DOCKERFILE_HOME>/files` and `<DOCKERFILE_HOME>/files/lib` respectively.

##### 3. Build the Docker image.

- Navigate to `<DOCKERFILE_HOME>` directory. <br>
  Execute `docker build` command as shown below.
    + `docker build -t siddhi-parser-alpine:v0.1.0 .`
    
##### 5. Running Docker image.

    + `docker run -it siddhi-parser-alpine:v0.1.0`

## Docker command usage references

* [Docker build command reference](https://docs.docker.com/engine/reference/commandline/build/)
* [Docker run command reference](https://docs.docker.com/engine/reference/run/)
* [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)