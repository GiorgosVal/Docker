`docker image tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]`<br/>
Creates an new image from the `SOURCE_IMAGE[:TAG]` named as `TARGET_IMAGE[:TAG]`. If tag is not specified, the default is latest.

>**Example:**<br/>
>```console
>$ docker image tag alpine myrepo/alpine
>$ docker image tag alpine:3.10 myrepo/alpine:3.10
>```
>
>After these commands if we do a `docker image ls` we'll see:
>```console
>REPOSITORY     TAG     IMAGE ID        CREATED         SIZE
>alpine         latest  d6e46aa2470d    3 weeks ago     5.57MB
>myrepo/alpine  latest  d6e46aa2470d    3 weeks ago     5.57MB
>alpine         3.10    be4e4bea2c2e    6 months ago    5.58MB
>myrepo/alpine  3.10    be4e4bea2c2e    6 months ago    5.58MB
>```
>
><br/>

---
`docker image push [OPTIONS] NAME[:TAG]`</br>
Pushes an image to a Docker Hub repository. Prerequisite, must be logged in to Docker Hub.
>**Example:**<br/>
>```console
>$ docker image push myrepo/alpine
>```
> Use `docker login` to log in to Docker Hub.
><br/>

---
`docker login [OPTIONS] [SERVER] [flags]`<br/>
`docker login [command]`<br/>
Login to Docker Hub (default), or to a server.
>**Warning:** Always logout from shared machines or servers when done. Sensitive information is stored in `~/.docker/config.json`.