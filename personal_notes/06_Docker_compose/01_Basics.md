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
  service_name: # a friendly name. this is also DNS name inside network
    image: # Optional if you use build:
    build: # Optional - creates an image
        context: # Either a path to a directory containing a Dockerfile, or a url to a git repository.
        dockerfile: # Alternate Dockerfile.
        args: # build arguments (must be declared in the Dockerfile)
        ...
    command: # Optional, replace the default CMD specified by the image
    environment: # Optional, same as -e in docker run
        - ENV_VAR_1: string
        - ENV_VAR_2: 'true'
        - ENV_VAR_3=string
        - ENV_VAR_4=true
    volumes: # Optional, same as -v in docker run
        - named_volume_data:/var/lib/postgresql/data
        - ./local/dir:/usr/local/container/dir/     # bind-mounting
    networks:
        # as string
        - some_net
        # as object
        - some_other_net:
            aliases:        # the service will be available as 'service_name',
                - alias1    # 'alias1', 'alias2' inside the network
                - alias2
    ports:
        # short syntax
        - "3000"
        - "3000-3005"
        - "8000:8000"
        - "9090-9091:8080-8081"
        - "49100:22"
        - "127.0.0.1:8001:8001"
        - "127.0.0.1:5000-5010:5000-5010"
        - "6060:6060/udp"
        - "12400-12500:1240"
        # long syntax
        - target: 80        # the port inside the container
          published: 8080   # the publicly exposed port
          protocol: tcp     # the port protocol (tcp or udp)
          mode: host        # 'host' for publishing a host port on each node,
                            # or 'ingress' for a swarm mode port to be load balanced.

  service_name_2:

volumes: # Optional, same as docker volume create
    named_volume_data:
networks: # Optional, same as docker network create
    some_net:
    some_other_net:
```

### Basic commands of docker-compose CLI tool
`docker-compose up`<br/>
Setups volumes, networks, etc, and starts all containers.

`docker-compose down`<br/>
Stops all containers and removes containers, volumes, networks.
> **Note:** Add the `-v` option to prune all volumes created by the docker-compose file.

`docker-compose ps`<br/>
Lists all containers running.

`docker-compose top`<br/>
Lists all services running inside the containers.