With containers it's easy to upgrade a database, e.g. from a patch version to another.

For example let's say we have a postgres 9.6.19 container that was creted with the following command:<br/>
```console
docker container run -d --name postgres -e POSTGRES_PASSWORD=mysecretpassword -v postgres:/var/lib/postgresql/data postgres:9.6.19
```

The command above created the named volume **postgres** (if not existent already).

To upgrade the postgres server version to 9.6.20 it is as easy as stopping the container, removing it(optional), and starting a new container that uses the same volume:

```console
$ docker container stop postgres

$ docker container rm postgres

$ docker container run -d --name postgres2 -e POSTGRES_PASSWORD=mysecretpassword -v postgres:/var/lib/postgresql/data postgres:9.6.20
```
In the container logs you'll see:<br/>
```console
PostgreSQL Database directory appears to contain a database; Skipping initialization
```

>**Note:**<br/>
>This works on patch versions. To upgrade to major/minor versions the DB may require a different upgrade path.