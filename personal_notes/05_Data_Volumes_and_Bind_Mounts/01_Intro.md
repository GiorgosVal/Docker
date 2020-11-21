## Points to remember
### Data Volumes
[Data Volumes](https://docs.docker.com/storage/volumes/) are special locations outside of the containers UFS (Union File SYstem) where Docker stores data. This configuration preserves the data across container removals and allows the attachment of any container to the data. Containers see the Data Volumes as a local file path. Contrary to the Bind Mounts, **Data Volumes create a new directory** within Docker's storage directory **on the host machine**, and Docker manages that directory's contents.

### Bind Mounts
Sharing or mounting a host directory or file, into a container. Containers see the [Bind Mounts](https://docs.docker.com/storage/bind-mounts/) as local directories or files. Contrary to the Data Volumes, **Bind Mounts do not create directories or files to the host, rather than sharing** host's directories and files.