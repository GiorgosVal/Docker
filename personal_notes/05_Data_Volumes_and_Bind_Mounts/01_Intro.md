## Points to remember
### Data Volumes
[Data Volumes](https://docs.docker.com/storage/volumes/) are special locations outside of the containers UFS (Union File SYstem) where Docker stores data. This configuration preserves the data across container removals and allows the attachment of any container to the data. Containers see the Data Volumes as a local file path. Contrary to the Bind Mounts, **Data Volumes create a new directory** within Docker's storage directory **on the host machine**, and Docker manages that directory's contents.

### Bind Mounts
Sharing or mounting a host directory or file, into a container. Containers see the [Bind Mounts](https://docs.docker.com/storage/bind-mounts/) as local directories or files. Contrary to the Data Volumes, **Bind Mounts do not create directories or files to the host, rather than sharing** host's directories and files.

>**Note:** When deploying a container with bind mounting, if the directory/file already exists in the container it is not actually deleted, but it is not seen by the container, since **the directory/file is mapped to that of the host**. On the other hand, the same container is deployed again but without bind mounting, then the already existing directories/files will be visible again.
>
>**Example:**
>Supposing that inside the **Dockerfile** from which the image was created has the instructions:
> ```dockerfile
> WORKDIR /usr/share/nginx/html
> COPY index.html index.html
>```
>This means that when the container is ran, there will be an existing file `/usr/share/nginx/html/index.html` inside the container. That **index.html** will be **a copy of another index.html** file placed in the relative path during the build procedure.<br/>
>
>Supposing now the same container is ran with bind mounting, with the option `-v$(pwd):/usr/share/nginx/html`. Supposing also that inside the host's `$(pwd)` the following file structure exists:
>
>```console
>pwd/
>    |
>    |--css/
>    |    |
>    |    |--mystyle.css
>    |
>    |--images/
>    |    |
>    |    |--image1.png
>    |    |--image2.png
>    |
>    |index.html
>```
>
>This means that when the container is ran, **the whole file structure above** will be available inside the container. Moreover, the container will have **read/write access** to that structure. So for example if a file is changed/deleted on the host, this will be immediately impact the container. And vice versa, if a file is changed/deleted on the container, this will impact the host too. **It is the same file after all.** 
><br/>
>

### Useful links
- [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)
- [Using volumes](https://docs.docker.com/storage/volumes/)
- [Using bind mounts](https://docs.docker.com/storage/bind-mounts/)


---
## Declaring volumes
### In the Dockerfile
`VOLUME ["/path/to/data"]`<br/>
When the container runs, a new volume location is created in the host and is assigned it to the specified directory inside the container.
>**Example:**<br/>
>The mysql Dockerfile has the instruction `VOLUME /var/lib/mysql`. When the container runs, it will create the new volume. If we inspect the container we'll see:
>```json
>"Volumes": {
>    "/var/lib/mysql": {}
>},
>```
>And also:
>```json
>"Mounts": [
>    {
>        "Type": "volume",
        >"Name": "3577665b9546967484975050bafaed5791ebc797f6ce7205c342c16a839dce72",
        >"Source": "/var/lib/docker/volumes/3577665b9546967484975050bafaed5791ebc797f6ce7205c342c16a839dce72/_data",
>        "Destination": "/var/lib/mysql",
>        "Driver": "local",
>        "Mode": "",
>        "RW": true,
>        "Propagation": ""
>    }
>],
>```
>In the above example, the `Destination` is the directory inside the container, and the `Source` is the directory in the host machine, where the data live.
><br/><br/>

>**Note for MacOS:**<br/>
>The above example will not work for Mac OS, because Mac isn't a real Docker host. Docker for Mac runs a virtual machine behind the scenes, so to access persistent volumes created by Docker for Mac, you need to log in that hidden virtual machine first.
>
>To enter the vm do:
>```console
>screen ~/Library/Containers/com.docker.docker/Data/vms/0/tty
>```
>Then pressing **Enter** you'll see a command line prompt `docker-desktop:~#`. From that point you're inside the Docker's VM and you can cd into the volumes with `cd /var/lib/docker/volumes`.<br/><br/>
>*Read more on this: [1](https://forums.docker.com/t/host-path-of-volume/12277), [2](https://timonweb.com/docker/getting-path-and-accessing-persistent-volumes-in-docker-for-mac/), [3](https://stackoverflow.com/questions/55603421/accessing-docker-volume-content-on-macos)*
><br/><br/>

### In the `docker container run` command and `-v` option
With the `-v` (or `--volume`) option we can specify:
1. either to **create a new unnamed** volume, like `-v /var/lib/mysql`
2. or to **create a new named** volume, like `-v mysqldb_data:/var/lib/mysql`
    - the 1st container run command will create the new `mysql_data` volume
3. or to **mount to an existing volume**, again like `-v mysqldb_data:/var/lib/mysql` or like `-v /mount/source/path:/var/lib/mysql`

### In the `docker container run` command and `--mount` option
The `--mount` option is the same as the `-v` option when doing mounting (case 3). The difference is that the source file path must be the **existing absolute file path** in the host.
>**Example:**<br/>
>```code
>--mount type=volume,src=-mysqldb_data,dst=/var/lib/mysql
>```
><br/>



### With the `docker volume create` command
With this command we can first create the volume, and use custom drivers and labels. After this we can execute the `docker run` command.

---
## Bind Mounting
### In the `docker container run` command and `-v` option
It is the same case as before, we do this like `-v /mount/source/path:/container/path`.
>**Example:**<br/>
>```console
>`docker container run -d --name nginx -p 80:80 -v $(pwd):/usr/share/nginx/html nginx`
>```
>With the above, our whole PWD is bind mounted inside the container.