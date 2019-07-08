# Dockerfiles for Siddhi Tooling #

This section defines the step-by-step instructions to build [Ubuntu](https://hub.docker.com/_/ubuntu/) Linux based Docker image for Siddhi Tooling Distribution 5.1.x.

## Prerequisites

* [Docker](https://www.docker.com/get-docker) v17.09.0 or above

## How to build the Siddhi Tooling images and run

### Building the Siddhi Tooling Base Image
Here we create a base image which contains the default released Siddhi Tooling distribution. 

##### 1. Checkout this repository into your local machine using the following Git command.

```
git clone https://github.com/siddhi-io/docker-siddhi.git
```

>The local copy of the `docker-files/siddhi-tooling/ubuntu` directory will be referred to as `DOCKERFILE_HOME` from this point onwards.

##### 2. Build the base Docker image.

- For base, navigate to `<DOCKERFILE_HOME>/base` directory. <br>
  Execute `docker build` command as shown below.
    + `docker build -t siddhiio/siddhi-tooling-base:5.1.x .`

### Building the Siddhi Tooling Image
Here we create the Siddhi Tooling image bundling the needed extensions and client jars.

Optional:  
> Use the `jartobundle.sh` script found in `siddhi-tooling-5.1.x/bin` as shown below; note that you will have to run this command for each jar you need to bundle in the image.

  ```
  ./siddhi-tooling-5.1.x/bin/jartobundle.sh path/to/kafka/client/jar <DOCKERFILE_HOME>/siddhi-tooling/files/lib
  ```        
##### 3. Build Docker image.

  Execute `docker build` command as shown below. 
    + `docker build -t siddhi-tooling:5.1.x .`
    
##### 4. Running Docker image.

    + `docker run -it -p 9390:9390 siddhi-tooling:5.1.x`    

## Docker command usage references

* [Docker build command reference](https://docs.docker.com/engine/reference/commandline/build/)
* [Docker run command reference](https://docs.docker.com/engine/reference/run/)
* [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)