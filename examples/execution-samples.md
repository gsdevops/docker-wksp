# Some sample of invocation examples

### TOC
* AWS S3 ls - cli with params
* Compilation with your choice of SDK Version
   
 
---

### AWS S3 ls - cli with params  (env vars)
we keep the credentials as local env vars and pass them to the docker container at exec time
```

docker run --rm -it -e AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID} -e AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}  amazon/aws-cli s3 ls

```



### Compilation with your choice of SDK Version  (filesystem sharing) 


#### Maven
Use container to compile code without installing anything locally.  This way you can choose the SDK version without installing it, and can switch easilly.  Also you can run the same compilation multiple times.   

download pet clinic sample:  
  `git clone https://github.com/gsdevops/spring-petclinic`  

in order to build the project (and use the ~/.m2 folder between invocations to save the cache)

``` shell
docker run -it --rm -v $PWD:/opt/app -w /opt/app -v $SOME_FOLDER/.m2:/root/.m2 maven:3.6.3-jdk-8-openj9 mvn clean

```
... now look at your `target` folder

#### Chef
```shell
docker run -t -v $PWD:/opt/mychef --rm   -e CHEF_WORK_ENV=Testing chef/chefdk:2.2.2  sh -c "/opt/mychef/single_chef_spec_from_docker.sh"
docker run -t -v $PWD:/opt/mychef --rm   -e CHEF_WORK_ENV=Testing chef/chefdk:3.1.0  sh -c "/opt/mychef/single_chef_spec_from_docker.sh"

```
