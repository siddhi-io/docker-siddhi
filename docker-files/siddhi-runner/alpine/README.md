# Dockerfiles for Siddhi Runner #

This section defines the step-by-step instructions to build [Ubuntu](https://hub.docker.com/_/ubuntu/) Linux based Docker image for Siddhi Runner Distribution 0.1.0.

## Prerequisites

* [Docker](https://www.docker.com/get-docker) v17.09.0 or above

## How to build the Siddhi Runner images and run

##### 1. Checkout this repository into your local machine using the following Git command.

```
git clone https://github.com/siddhi-io/docker-siddhi.git
```

>The local copy of the `dockerfiles/alpine` directory will be referred to as `DOCKERFILE_HOME` from this point onwards.

##### 2. If you need to use the Siddhi Runner distribution that is locally available, copy the distribution to `<DOCKERFILE_HOME>/base/files`.

##### 3. Build the base Docker image.

- For base, navigate to `<DOCKERFILE_HOME>/base` directory. <br>
  Execute `docker build` command as shown below.
    + `docker build -t siddhi-runner-base:0.1.0 .`

##### 4. Convert and copy the needed client jars and extensions to `<DOCKERFILE_HOME>/base/files/lib` directory

> Use the `jartobundle.sh` script found it `siddhi-runner-0.1.0/bin` as shown below; note that you will have to run this command for each jar mentioned above

  ```
  ./siddhi-runner-0.1.0/bin/jartobundle.sh path/to/kafka/client/jar <DOCKERFILE_HOME>/siddhi-runner/files/lib
  ```        
##### 5. Build Docker image.

  Execute `docker build` command as shown below. 
    + `docker build -t siddhi-runner:0.1.0 .`
    
##### 6. Running Docker image.

    + `docker run -it siddhi-runner:0.1.0`

## Docker command usage references

* [Docker build command reference](https://docs.docker.com/engine/reference/commandline/build/)
* [Docker run command reference](https://docs.docker.com/engine/reference/run/)
* [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)