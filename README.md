# docker-wksp
  
  
  
### Docker cli  
* [Docker build](https://docs.docker.com/engine/reference/commandline/build/) - `docker build -t TAG:LABEL [PATH | URL]`
* [Docker run](https://docs.docker.com/engine/reference/commandline/eun/) - `docker run --rm -it -v $HOST_PATH:$CONTAINER_PATH -e ENV_VAR:$ENV_VALUE IMAGE:LABEL [COMMAND]`
* [Docker exec](https://docs.docker.com/engine/reference/commandline/exec/)
* 



### Dockerfile commands:
[Dockerfile reference](https://docs.docker.com/engine/reference/builder/)  

* RUN - run a command
* ENV - declare an env var
* ARG - declare a build time arg
* ADD / COPY - copy files/directories
* VOLUME - create a mountpoint
* WORKDIR - defines the working directory
* ONBUILD - events for future derived image build
* 