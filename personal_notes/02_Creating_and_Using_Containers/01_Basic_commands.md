`docker`<br/>
Just type this and you'll get a list of the available docker commands.

The old structure of the docker commands is:

`docker <command> (options)`
> e.g.: `docker run`

The new structure of the docker commands is:

`docker (<management-command> <sub-command>) (options)`
> e.g.: `docker container run`

---
`docker version`<br/>
Shows the version of the client and sever. 

Also verifies that the client can talk to the server.

---
`docker info`<br/>
Shows a detailed list of various configuration values of the engine.

---
`docker container run --publish <ext-port>:<int-port> --detach --name <name> <image:version>`<br/>
This command:
- Searches locally to find the image version given
- If the image is not found locally, searches in Docker Hub and downloads the image version
- Creates **a new** container from that image and prepares it to start
- Gives that container the name specified after the `--name` option
- Gives the container a virtual IP on a private network inside the docker engine
- Opens up a port on the host (ext-port) and forwards the traffic to the port in the container (int-port).
- Starts the container by using the CMD in the image Dockerfile.
- The `--detach` tells the docker to run in the background, and returns the docker container id.

>**Example:**
>
>`docker container run --publish 80:80 --detach --name myhost nginx:1.17.0`
>
>`docker container run -p 80:80 -d --name myhost nginx:1.17.0`
>
>This starts a new nginx instance listening on port 80, so it can be access at http://localhost:80/
>
>**Note 1:** `CTRL + C` stops a running container<br/>
>**Note 2:** This command always starts a new container.<br/>
>**Note 3:** I f a running container already uses this port, we'll get an error.<br/>
>**Note 4:** If you don't specify `--name` a random name will be given to the container.<br/>
>**Note 5:** If you don't specify `--detach` after executing the command you'll see (and follow) the logs of the container.<br/>
>**Note 6:** If you don't specify `:version` Docker will download the latest version of the image.<br/>
>**Note 7:** Generic usage: `docker container run [OPTIONS] IMAGE [COMMAND] [ARG...]`
>**Note 8:** For more info: `docker container run --help`
><br>

---
`docker container stop <container id>`<br/>
`docker container stop <container name>`<br/>
Stops the container with the id/name given. **There's no need** to provide the full container id.

>**Examples:**
>
>All commands will work
>
>`docker container stop 2edf15a9cb603cf482591be3dba6d50b16416f74254f49efae527f390be7e904`
>
>`docker container stop 2edf15`
>
>`docker container stop fervent_grothendieck`<br/>
><br>
---
`docker container ls`<br/>
`docker container ps`<br/>
Shows the containers running.
>**Note:** Add the option `-a` to see all containers.

---
`docker image ls`<br/>
Shows the images.
>**Note:** Add the option `-a` to see more images.

---
`docker container start <container id>`<br/>
`docker container start <container name>`<br/>
Starts a previously stopped container with the id/name given. **There's no need** to provide the full container id.

>**Examples:**
>
>All commands will work
>
>`docker container start 2edf15a9cb603cf482591be3dba6d50b16416f74254f49efae527f390be7e904`
>
>`docker container start 2edf15`
>
>`docker container start fervent_grothendieck`<br/>
><br>

---
`docker container logs <container id>`<br/>
`docker container logs <container name>`<br/>
Shows **the latest logs** of the container with the id/name given. **There's no need** to provide the full container id.

>**Examples:**
>
>All commands will work
>
>`docker container logs 2edf15a9cb603cf482591be3dba6d50b16416f74254f49efae527f390be7e904`
>
>`docker container logs 2edf15`
>
>`docker container logs fervent_grothendieck`<br/>
><br>


>**Note 1:** Add the option `-f` to follow the logs.<br/>
>**Note 2:** Add the option `--help` to see other options.<br/>
><br>

---
`docker container top <container id>`<br/>
`docker container top <container name>`<br/>
Shows the processes running inside the container with the id/name given. **There's no need** to provide the full container id.

>**Examples:**
>
>All commands will work
>
>`docker container top 2edf15a9cb603cf482591be3dba6d50b16416f74254f49efae527f390be7e904`
>
>`docker container top 2edf15`
>
>`docker container top fervent_grothendieck`<br/>
><br>

---
`docker container rm <...container ids>`<br/>
`docker container rm <...container names>`<br/>
`docker container rm <...container ids or names>`<br/>
Removes **(only) the stopped** containers with the specified id/name.

>**Example:**
>
>`docker container rm brave_moore 4a6d54769caf`<br/>
><br>

>**Note 1:** Add the option `-f` to force rm the containers, even if they are running.<br/>
><br>

---
## Other examples
## MySQL
`docker container run -d -p 3306:3306 --name db -e MYSQL_RANDOM_ROOT_PASSWORD=yes mysql/mysql-server:5.7.32`

## Nginx
`docker run -d -p 80:80 --name proxy nginx`

## Httpd
`docker run -d -p 8080:80 --name webserver httpd`

## Ubuntu
`docker container run -it --name ubuntu ubuntu`<br/>
To run it and enter it's shell.

`docker container run -it -d --name ubuntu ubuntu`<br/>
To detach.

## Alpine Linux
`docker container run -it --name alpine alpine sh`<br/>
To run it and enter it's shell.

`docker container run -it -d --name alpine alpine`<br/>
To detach.