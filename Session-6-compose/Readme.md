# Session 6 - Docker Compose



### General Docker compose
Reference: [compose-file format ](https://docs.docker.com/compose/compose-file/)  
  
dependencies - https://docs.docker.com/compose/compose-file/compose-file-v3/#depends_on  
inject env - https://docs.docker.com/compose/compose-file/compose-file-v3/#env_file  
mount file(systems) - https://docs.docker.com/compose/compose-file/compose-file-v3/#volumes  

In this session we will create a multiple container system, using `docker-compose` that consists of a small 3 tier web application containing a database and a web application.

For this we will use a forked repo from the Spring Samples.  
clone the following repo:  
`git clone git@github.com:gsdevops/spring-petclinic.git`  

This repo is a Java based repo.

### Step 1: Build the JAR
The general command is 
`mvn clean install -Dmaven.test.skip`

docker run -it --rm -v $PWD:/opt/app -w /opt/app -v $SOME_FOLDER/.m2:/root/.m2  maven:3.8.3 mvn clean install  -Dmaven.test.skip

look at folder `target` and search for a file named similar to `spring-petclinic-2.4.2.jar`.


### Step 2: Connect as Regular process

Set JAR configuration to point to Database


### Step 3:  Start as docker compose

