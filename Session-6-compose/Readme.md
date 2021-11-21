# Session 6 - Docker Compose



### General Docker compose
Reference: [compose-file format ](https://docs.docker.com/compose/compose-file/)  

In this session we will create a multiple container system, using `docker-compose` that consists of a small 3 tier web application containing a database and a web application.
  
For this we will use a forked repo from the Spring Samples.  
clone the following repo:  
`git clone git@github.com:gsdevops/spring-petclinic.git`  

This repo is a Java based repo.

### Step 1: Build the image
The general command is 
`mvn clean install -Dmaven.test.skip`

docker run -it --rm -v $PWD:/opt/app -w /opt/app -v $SOME_FOLDER/.m2:/root/.m2  maven:3.8.3 mvn clean install  -Dmaven.test.skip

  