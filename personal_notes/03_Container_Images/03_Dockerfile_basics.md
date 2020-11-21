## Useful links
[Dockerfile reference](https://docs.docker.com/engine/reference/builder/)

---
## Dockerfile

### What is
A Dockerfile is a special file which is used to build images. It is something like a script with instructions that have a special meaning.

### Instructions
`FROM <image:version>`<br/>
Image to pull and start building. To start with a truly empty container, use `FROM scratch`.

`ENV VARIABLE_NAME value`</br>
Specify Environment Variables as key/value pairs so as to inject them later in the script, and also use them as envvar when the container is running.

`RUN [...shell commands>]`<br/>
It runs shell commands inside the container while it is building it. Usually for installing software from a package repo, do unzipping, file edits, run shell scripts that were copied earlier in the file, etc, and generally any commands you can access from inside the container **at the specific time**.
>**Best practice:** Chain the multiple shell commands with `&&`, so as all the commands of a `RUN` command will fit into a single layer. For example:
>
>```
> RUN apt-get update && \
>       apt-get install something && \
>       rm -rf /var/lib/apt/lists/*
>```
><br/>

`EXPOSE [...ports]`<br/>
Which ports to expose **in the container**. By default the container does not expose any port inside the virtual network, unless listed here. The `-p` option still will be needed to open/forward these ports on the host,when we use `docker run`.

`CMD ["nginx", "-g", "daemon off;]`<br/>
The command that will run every time we run a new container or restart a stopped container. **Only one `CMD`** command is allowed (the last one in the file wins).


### How to build images
`docker image build -f /path/to/a/Dockerfile -t <repo>/<image>:<version> <context>`<br/>
Builds the image:
- Using the Dockerfile in the path after the `-f` option
- Stores it in a path
- If the build succeeds, tags it and uploads it to the repo specified
>**Examples:**
>```console
>docker image build .
>```
>Builds the image using the `PWD/Dockerfile` in the PWD context.
>```console
>docker image build -f ~/Projects/Docker/nginx/Dockerfile -t customnginx .
>```
>Builds the image using the Dockerfile specified, and tags it as `customnginx:latest`.
>```console
>docker image build -t gvalrepo/customnginx:3.2 -t gvalrepo/customnginx:latest .
>```
>Builds the image using the Dockerfile specified, tags it as `customnginx:3.2`, `customnginx:latest` and uploads it to the `gvalrepo`.

### Best practices

#### Frequent changes on bottom
Place **as close to the top** of the Dockerfile the code that changes **less often**.
Place **as close to the bottom** of the Dockerfile the code that changes **frequently**.
This way, each time a change is made, Docker won't have to rebuilt each image layer but will use the cached layers.

#### Chain shell commands
Use the `&&` to chain shell commands. This way only one image layer will be created from a bunch of chained shell commands.