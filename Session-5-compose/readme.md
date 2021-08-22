
# Docker Compose

[Docker compose](https://docs.docker.com/compose/) is a basic multiple container applications.


## Main use cases (for us)
* Develop components in a multiple-component system; for example when you need several additional servers to operate (redis, rest api, database)
* CI - set a system with all components on a single host for integration / system testing
* Multiple isolated environments on same server 


## Setup
installation:  
[https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)
```shell
```

## Concepts
Docker compose is a single node orchestrator:
* starts / stops containers
* assigns ports / ip addresses
* assigns containers to ports
* dependencies in service start
* use of a `.env` file - for quick adjustments (also `--env-file`)





## Links

https://docs.docker.com/compose/  
