`docker system df`<br/>
Shows the space used for each docker fragment.
>**Example:**
>```console
>TYPE           TOTAL   ACTIVE  SIZE        RECLAIMABLE
>Images         24      11      13.45GB     1.596GB (11%)
>Containers     15      0       4.86GB      4.86GB (100%)
>Local Volumes  18      10      5.886GB     397.3MB (6%)
>Build Cache    0       0       0B          0B
>```
><br/>

`docker system prune`<br/>
Clears everything that is reclaimable. Specifically removes:
- all stopped containers
- all networks not used by at least one container
- all dangling images (image layers not related to the existing images)
- all dangling build cache

`docker system prune -a`<br/>
Clears everything. Specifically removes:
- all stopped containers
- all networks not used by at least one container
- all images without at least one container associated to them
- all build cache

If we want to clear only selected fragments:<br/>
`docker image prune`<br/>
`docker image prune -a`<br/>

`docker container prune`<br/>
`docker container prune -a`<br/>

`docker volume prune`<br/>
`docker network prune`<br/>



