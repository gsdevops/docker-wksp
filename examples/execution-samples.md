# Some sample of invocation examples
    

* pass credentials as env vars
```

docker run --rm -it -e AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID} -e AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}  amazon/aws-cli s3 ls

```



* Use container to compile code without installing anything  
download pet clinic sample:  
  `git clone https://github.com/gsdevops/spring-petclinic`  

in order to build the project (and use the ~/.m2 folder between invocations to save the cache)

``` shell
docker run -it --rm -v $PWD:/opt/app -w /opt/app -v $PWD/.m2:/root/.m2 maven:3.6.3-jdk-8-openj9 mvn clean
```
... now look at your `target` folder

