# Points to remember
When a container starts by default it connects to a particular private virtual docker network called "bridge".

Each virtual network routes out through NAT firewall on host IP. This NAT firewall is actually the docker daemon configuring the host IP address, so that the containers can get out on the internet.

We don't need to use the `-p` when we have specific containers that want to talk to each other inside the same virtual network.

Best practice is to create a new virtual network for each app. Example:
- Application 1
    - network "my_web_app"
    - mysql container
    - php/apache container
- Application 2
    - network "my_api"
    - mongo container
    - nodejs container

Here's an example visualization of the bridge network that has two containers inside it.
![](defaultBridgeNetworkDocker.png)
*Source: [dev.vividbreeze.com](https://dev.vividbreeze.com/docker-networking-bridge-network/)*

In the above example:
- **nginx1** can talk to **nginx2** directly with their private IPs
- access to the **nginx1** from outside the bridge network is made with the IP/port 192.168.0.6:3001

## Default networks
- **bridge:**
The Docker default virtual network which is NAT'ed behind the host IP.
- **host:**
Skips the Docker virtual networking and attaches a container directly to the hosts interface. It gains performance but sacrifices security of container model.
- **none:**
Removes eth0 and leaves us with localhost interface in a container. It is equivalent to having an interface that is not attached to anything.

## Network drivers
Built-in or 3rd party extensions that provide virtual network features.
### Default drivers
- **bridge:** A simple driver that creates a virtual network locally with its own subnet somewhere around 172.17.x.x. It does not provide advanced features like overlay networks (allow private networking between hosts), or other 3rd party drivers like Weave.

## DNS
Since things in containers are dynamic, we can't rely on IP addresses inside the containers. On the other hand, static IP's and using IP's for talking to containers is an anti-pattern. A good DNS is important. Docker daemon has a buil-in DNS server that uses the container names as the equivalent to a host name.

When we create a network:
- by default all containers attached, can talk to each other by using their names
- we can also define alias and use them instead of names

For the default bridge network:
- containers can only talk to each other using IPs. A legacy `--link` option was used to create links between the containers, **but this is not recommended**. It is better to create our own networks.

### DNS Round Robin
We can have multiple containers on a created network respond to tha same DNS address. To do this we use the `--network-alias` option of the `docker container run` command.

---
`docker container port <container>`<br/>
See the ports that are open in a container.
>**Example:**<br/>
>`$ docker container port mysql8`<br/>

---
`docker container inspect --format '{{ .NetworkSettings.IPAddress}}' <container>`<br/>
Returns the `$.NetworkSettings.IPAddress` value of the JSON response of the `docker container inspect`.

>**Example:**<br/>
>`docker container inspect --format '{{ .NetworkSettings.IPAddress}}' mysql8`<br/>

---
`docker network ls`<br/>
Lists the available networks.

<details>
<summary>Example output</summary>

```console
NETWORK ID          NAME                          DRIVER              SCOPE
b549f8c21c32        bridge                        bridge              local
ec2525a5de1d        host                          host                local
d18acb692139        none                          null                local
```
</details>

---
`docker network inspect [OPTIONS] NETWORK [NETWORK...]`<br/>
Shows details about a specific network.

>**Example:**<br/>
>`docker network inspect bridge`<br/>
><details open>
><summary>Example output</summary>
>
>```json
>[
>    {
>        "Name": "bridge",
>        "Id": "b549f8c21c32e4f436318d35e9fe88f1b6fcf4e0d14c241a8cb3a5ba60349c2b",
>        "Created": "2020-11-10T20:10:30.018815933Z",
>        "Scope": "local",
>        "Driver": "bridge",
>        "EnableIPv6": false,
>        "IPAM": {
>            "Driver": "default",
>            "Options": null,
>            "Config": [
>                {
>                    "Subnet": "172.17.0.0/16",
>                    "Gateway": "172.17.0.1"
>                }
>            ]
>        },
>        "Internal": false,
>        "Attachable": false,
>        "Ingress": false,
>        "ConfigFrom": {
>            "Network": ""
>        },
>        "ConfigOnly": false,
>        "Containers": {
>            "6cdb8c7d8ea983d70c06c99285813844d5442ed1da49fdf4ecb8d63226407038": {
>                "Name": "mysql8_from_upgrade",
                >"EndpointID": "b4064ace59d14f1c9bfd6c8de3ff6f71edf19df22c714f5b3b2ecaed77c02cd4",
>                "MacAddress": "02:42:ac:11:00:02",
>                "IPv4Address": "172.17.0.2/16",
>                "IPv6Address": ""
>            },
>            "d8abbc6b7a9443b4fde7fdf747c5f305b5f2bbed59a17813b37a2a9a9cbf9eac": {
>                "Name": "nginx",
                >"EndpointID": "8ef3a2115d6bf087aa1f357a3290172642178f2ea4fbcb133da4e0cf0f877722",
>                "MacAddress": "02:42:ac:11:00:04",
>                "IPv4Address": "172.17.0.4/16",
>                "IPv6Address": ""
>            },
>            "fbf2de3f074a08b16eed0aa6587d76afed157e5077959361365524f122d210ed": {
>                "Name": "alpine",
                >"EndpointID": "54c57be1f1db4d1df7944fa8c8303a86489cdc34b0ce65f269ebaa8d411dbb89",
>                "MacAddress": "02:42:ac:11:00:03",
>                "IPv4Address": "172.17.0.3/16",
>                "IPv6Address": ""
>            }
>        },
>        "Options": {
>            "com.docker.network.bridge.default_bridge": "true",
>            "com.docker.network.bridge.enable_icc": "true",
>            "com.docker.network.bridge.enable_ip_masquerade": "true",
>            "com.docker.network.bridge.host_binding_ipv4": "0.0.0.0",
>            "com.docker.network.bridge.name": "docker0",
>            "com.docker.network.driver.mtu": "1500"
>        },
>        "Labels": {}
>    }
>]
>```
></details>
><br/>

---
`docker network create [OPTIONS] NETWORK`<br/>
Creates a new network.
>**Example:**<br/>
>`docker network create my_network`<br/>
>**Note:** This will create a network using the default `bridge` driver. Doing an `docker network ls` will output:<br/>
>```console
>ec2525a5de1d        host                          host                local
>```
><br/>

---
`docker container run -d --name <name> --network <network> --network-alias <alias> <image>`<br/>
Starts a new container and attaches it to a network. It associates this container with a network alias.
>**Example:** Creating a DNS Round Robin<br/>
>```bash
># first create a network
>$ docker network create my_network
>
># create two elasticsearch containers - attach them to the network - associate them with the same network alias
>$ docker container run -d --network my_network --network-alias search elasticsearch:2
>$ docker container run -d --network my_network --network-alias search elasticsearch:2
>
># see the containers
> $ docker container ps
>CONTAINER ID        IMAGE                       COMMAND                  CREATED             STATUS                PORTS                               NAMES
>6a8d851ffcbb        elasticsearch:2             "/docker-entrypoint.…"   16 minutes ago      Up 16 minutes         9200/tcp, 9300/tcp                  confident_shockley
>980c2b204014        elasticsearch:2             "/docker-entrypoint.…"   16 minutes ago      Up 16 minutes         9200/tcp, 9300/tcp                  cool_ritchie
>
># create an alpine container - attach it to the network - perform an nslookup using the network alias
>$ docker container run --rm --network my_network alpine:3.10 nslookup search
>
>Name:      search
>Address 1: 172.25.0.3 search.my_network
>Address 2: 172.25.0.2 search.my_network
>
># create a centos container - attach it to the network - curl the 'search' host to the default 9200 port
>$ docker container run --network my_network --rm centos curl -s search:9200
> # To see the DNS Round Robin in action, execute the above command many times, and notice that the container is randomly chosen. For example:
> # Output for the 172.25.0.2 search.my_network
>{
>  "name" : "Robert \"Bobby\" Drake",
>  "cluster_name" : "elasticsearch",
>  "cluster_uuid" : "bu7pAMkHQ9K5rbDYylT1-A",
>  "version" : {
>    "number" : "2.4.6",
>    "build_hash" : "5376dca9f70f3abef96a77f4bb22720ace8240fd",
>    "build_timestamp" : "2017-07-18T12:17:44Z",
>    "build_snapshot" : false,
>    "lucene_version" : "5.5.4"
>  },
>  "tagline" : "You Know, for Search"
>}
> # Output for the 172.25.0.3 search.my_network
>{
>  "name" : "Cyborg X",
>  "cluster_name" : "elasticsearch",
>  "cluster_uuid" : "NPmMg1EkQZuTF5WjPtN2pg",
>  "version" : {
>    "number" : "2.4.6",
>    "build_hash" : "5376dca9f70f3abef96a77f4bb22720ace8240fd",
>    "build_timestamp" : "2017-07-18T12:17:44Z",
>    "build_snapshot" : false,
>    "lucene_version" : "5.5.4"
>  },
>  "tagline" : "You Know, for Search"
>}
>```
><br/>

---
`docker network connect [OPTIONS] NETWORK CONTAINER`<br/>
Attaches an already running container to a network. It **does not detach it** from a previously attached network. Dynamically creates a NIC in a container on an existing virtual network.
>**Example:**<br/>
>`docker network connect my_network alpine`
>Before the execution of the above command, the `alpine` container was attached to the `bridge` network. After the execution of the command, the `alpine` container was attached to both the `bridge` and the `my_network` networks.

---
`docker network disconnect [OPTIONS] NETWORK CONTAINER`<br/>
Detaches an already running container from a network.

---
