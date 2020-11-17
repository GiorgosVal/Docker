## Points to remember
1. The containers run as long as the command that ran on startup runs.
2. Usage: `docker container run [OPTIONS] IMAGE [COMMAND] [ARG...]`
3. As long as we enter the shell of a container, we can do any administrative work we can do in any shell (e.g. install curl command). This work will be available only in the specific container.

---
`$ docker container run -it --name <container_name> <image> bash`<br/>
Starts a new container interactively (enters its shell).

>**Example:**<br/>
>`$ docker container run -it --name proxy nginx bash`<br/>
>Example output:
>```console
>root@d8abbc6b7a94:/#
>```
><br/>

>**Note 1:**<br/>
> `t`: Allocates a pseudo-TTY. Simulates a real terminal, like what SSH does.<br/>
> `i`: Keep STDIN open even if not attached. Keeps session open to receive terminal input.<br/>
> `bash`: The default shell. Also this is the argument passed in the `docker run` command.

>**Note 2:**<br/>
>Executing a `docker container inspect proxy` and searching in the response we'll find:
>```json
>"Cmd": [
>    "bash"
>],
>```
>This is the command that we configured to ran on startup. This means that when we exit the bash, the container will stop.

---
`$ docker container start -ai <container>`<br/>
Start again a previously stop container and enter its shell.
>**Example:**<br/>
>`$ docker container start -ai ubuntu`<br/>

---
`$ docker container exec -it <container> bash`<br/>
Runs a command in **existing** container. Enters the shell of an already running container.

>**Example:**<br/>
>`$ docker container exec -it ubuntu bash`<br/>