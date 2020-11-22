## What is Docker compose
A configuration file, where we can configure relationships between containers and save our docker container run settings. It is comprised be 2 separate but related things:
- A YAML file, where we configure:
    - which containers to run
    - environment variables
    - networks
    - volumes
    - etc
- A CLI tool `docker-compose` that uses that yml file.

### Useful links
- [Overview of Docker Compose
](https://docs.docker.com/compose/)
- [Docker compose file reference](https://docs.docker.com/compose/compose-file/)

### Example structure of docker-compose.yml

The default name is `docker-compose.yml`, but we can use the `-f` flag to specify whatever filename we want.

Here's a template:
```yml
version: '3.1'  # if no version is specified then v1 is assumed. Recommend v2 minimum

services:  # containers. same as docker run
  servicename: # a friendly name. this is also DNS name inside network
    image: # Optional if you use build:
    command: # Optional, replace the default CMD specified by the image
    environment: # Optional, same as -e in docker run
    volumes: # Optional, same as -v in docker run
  servicename2:

volumes: # Optional, same as docker volume create

networks: # Optional, same as docker network create
```

### Basic commands of docker-compose CLI tool
`docker-compose up`<br/>
Setups volumes, networks, etc, and starts all containers.

`docker-compose down`<br/>
Stops all containers and removes containers, volumes, networks.

`docker-compose ps`<br/>
Lists all containers running.

`docker-compose top`<br/>
Lists all services running inside the containers.