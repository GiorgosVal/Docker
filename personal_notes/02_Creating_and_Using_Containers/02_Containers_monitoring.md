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
>`docker container top mysql_mysql_8_0_21_1`<br/>
><br>
>Example output:
>```console
>$ docker container top mysql_mysql_8_0_21_1
>PID                 USER                TIME                COMMAND
>80135               root                0:00                {entrypoint.sh} /bin/bash /entrypoint.sh mysqld
>80290               27                  22:52               mysqld
>```
><br/>

---
`docker container inspect <container id>`<br/>
`docker container inspect <container name>`<br/>
Returns metadata in JSON format, about the container (startup, config, volumes, networking, etc).

>**Example:**
>
>`docker container inspect mysql_mysql_8_0_21_1`
>
> Example output:
><details>
>
>```json
>[
>    {
>        "Id": "f28e9dc04359b8af6668fcf35baf3cff7fd8bbf2fc9d0c7e63a38a44c3a4a1fd",
>        "Created": "2020-11-12T08:25:32.1217211Z",
>        "Path": "/entrypoint.sh",
>        "Args": [
>            "mysqld"
>        ],
>        "State": {
>            "Status": "running",
>            "Running": true,
>            "Paused": false,
>            "Restarting": false,
>            "OOMKilled": false,
>            "Dead": false,
>            "Pid": 80135,
>            "ExitCode": 0,
>            "Error": "",
>            "StartedAt": "2020-11-12T08:25:33.6524499Z",
>            "FinishedAt": "0001-01-01T00:00:00Z",
>            "Health": {
>                "Status": "healthy",
>                "FailingStreak": 0,
>                "Log": [
>                    {
>                        "Start": "2020-11-12T19:38:30.913655Z",
>                        "End": "2020-11-12T19:38:31.1735341Z",
>                        "ExitCode": 0,
>                        "Output": "mysqld is alive\n"
>                    },
>                    {
>                        "Start": "2020-11-12T19:39:01.170548Z",
>                        "End": "2020-11-12T19:39:01.4946078Z",
>                        "ExitCode": 0,
>                        "Output": "mysqld is alive\n"
>                    },
>                    {
>                        "Start": "2020-11-12T19:39:31.5018933Z",
>                        "End": "2020-11-12T19:39:31.9942872Z",
>                        "ExitCode": 0,
>                        "Output": "mysqld is alive\n"
>                    },
>                    {
>                        "Start": "2020-11-12T19:40:02.0093547Z",
>                        "End": "2020-11-12T19:40:02.3742275Z",
>                        "ExitCode": 0,
>                        "Output": "mysqld is alive\n"
>                    },
>                    {
>                        "Start": "2020-11-12T19:40:32.3659985Z",
>                        "End": "2020-11-12T19:40:32.5355109Z",
>                        "ExitCode": 0,
>                        "Output": "mysqld is alive\n"
>                    }
>                ]
>            }
>        },
>        "Image": "sha256:8a3a24ad33bed49abe5fef7a1f1ea88b7bee7905f25c64f945cdc34925031b1a",
        >"ResolvConfPath": "/var/lib/docker/containers/f28e9dc04359b8af6668fcf35baf3cff7fd8bbf2fc9d0c7e63a38a44c3a4a1fd/resolv.conf",
        >"HostnamePath": "/var/lib/docker/containers/f28e9dc04359b8af6668fcf35baf3cff7fd8bbf2fc9d0c7e63a38a44c3a4a1fd/hostname",
        >"HostsPath": "/var/lib/docker/containers/f28e9dc04359b8af6668fcf35baf3cff7fd8bbf2fc9d0c7e63a38a44c3a4a1fd/hosts",
        >"LogPath": "/var/lib/docker/containers/f28e9dc04359b8af6668fcf35baf3cff7fd8bbf2fc9d0c7e63a38a44c3a4a1fd/f28e9dc04359b8af6668fcf35baf3cff7fd8bbf2fc9d0c7e63a38a44c3a4a1fd-json.log",
>        "Name": "/mysql_mysql_8_0_21_1",
>        "RestartCount": 0,
>        "Driver": "overlay2",
>        "Platform": "linux",
>        "MountLabel": "",
>        "ProcessLabel": "",
>        "AppArmorProfile": "",
>        "ExecIDs": null,
>        "HostConfig": {
>            "Binds": [
>                "mysql_mysql_8_0_21_data:/var/lib/mysql:rw"
>            ],
>            "ContainerIDFile": "",
>            "LogConfig": {
>                "Type": "json-file",
>                "Config": {}
>            },
>            "NetworkMode": "mysql_default",
>            "PortBindings": {
>                "3306/tcp": [
>                    {
>                        "HostIp": "",
>                        "HostPort": "3308"
>                    }
>                ]
>            },
>            "RestartPolicy": {
>                "Name": "",
>                "MaximumRetryCount": 0
>            },
>            "AutoRemove": false,
>            "VolumeDriver": "",
>            "VolumesFrom": [],
>            "CapAdd": null,
>            "CapDrop": null,
>            "Capabilities": null,
>            "Dns": null,
>            "DnsOptions": null,
>            "DnsSearch": null,
>            "ExtraHosts": null,
>            "GroupAdd": null,
>            "IpcMode": "private",
>            "Cgroup": "",
>            "Links": null,
>            "OomScoreAdj": 0,
>            "PidMode": "",
>            "Privileged": false,
>            "PublishAllPorts": false,
>            "ReadonlyRootfs": false,
>            "SecurityOpt": null,
>            "UTSMode": "",
>            "UsernsMode": "",
>            "ShmSize": 67108864,
>            "Runtime": "runc",
>            "ConsoleSize": [
>                0,
>                0
>            ],
>            "Isolation": "",
>            "CpuShares": 0,
>            "Memory": 0,
>            "NanoCpus": 0,
>            "CgroupParent": "",
>            "BlkioWeight": 0,
>            "BlkioWeightDevice": null,
>            "BlkioDeviceReadBps": null,
>            "BlkioDeviceWriteBps": null,
>            "BlkioDeviceReadIOps": null,
>            "BlkioDeviceWriteIOps": null,
>            "CpuPeriod": 0,
>            "CpuQuota": 0,
>            "CpuRealtimePeriod": 0,
>            "CpuRealtimeRuntime": 0,
>            "CpusetCpus": "",
>            "CpusetMems": "",
>            "Devices": null,
>            "DeviceCgroupRules": null,
>            "DeviceRequests": null,
>            "KernelMemory": 0,
>            "KernelMemoryTCP": 0,
>            "MemoryReservation": 0,
>            "MemorySwap": 0,
>            "MemorySwappiness": null,
>            "OomKillDisable": false,
>            "PidsLimit": null,
>            "Ulimits": null,
>            "CpuCount": 0,
>            "CpuPercent": 0,
>            "IOMaximumIOps": 0,
>            "IOMaximumBandwidth": 0,
>            "MaskedPaths": [
>                "/proc/asound",
>                "/proc/acpi",
>                "/proc/kcore",
>                "/proc/keys",
>                "/proc/latency_stats",
>                "/proc/timer_list",
>                "/proc/timer_stats",
>                "/proc/sched_debug",
>                "/proc/scsi",
>                "/sys/firmware"
>            ],
>            "ReadonlyPaths": [
>                "/proc/bus",
>                "/proc/fs",
>                "/proc/irq",
>                "/proc/sys",
>                "/proc/sysrq-trigger"
>            ]
>        },
>        "GraphDriver": {
>            "Data": {
                >"LowerDir": "/var/lib/docker/overlay2/bee30e1ba33befb36d76db325d72c565a9cac19ea53f705ccce6f64277781817-init/diff:/var/lib/docker/overlay2/0f9aa5b2c91cce0a9531088be214901fa5f422351db26224ae49feb1272b30a2/diff:/var/lib/docker/overlay2/60a646ba05e0560442b75650b09bc3a8a39e32b7170f3774f85cf4db1618f061/diff:/var/lib/docker/overlay2/5efd1b2edfa5370e74562f56adebb2712e861d8802acbf4ef343f9421321906c/diff:/var/lib/docker/overlay2/dbd0d23b0ebc198827d34e72e262f3e59dd3dc5bff784769930c0b1b11563da1/diff",
                >"MergedDir": "/var/lib/docker/overlay2/bee30e1ba33befb36d76db325d72c565a9cac19ea53f705ccce6f64277781817/merged",
                >"UpperDir": "/var/lib/docker/overlay2/bee30e1ba33befb36d76db325d72c565a9cac19ea53f705ccce6f64277781817/diff",
                >"WorkDir": "/var/lib/docker/overlay2/bee30e1ba33befb36d76db325d72c565a9cac19ea53f705ccce6f64277781817/work"
>            },
>            "Name": "overlay2"
>        },
>        "Mounts": [
>            {
>                "Type": "volume",
>                "Name": "mysql_mysql_8_0_21_data",
>                "Source": "/var/lib/docker/volumes/mysql_mysql_8_0_21_data/_data",
>                "Destination": "/var/lib/mysql",
>                "Driver": "local",
>                "Mode": "rw",
>                "RW": true,
>                "Propagation": ""
>            }
>        ],
>        "Config": {
>            "Hostname": "f28e9dc04359",
>            "Domainname": "",
>            "User": "",
>            "AttachStdin": false,
>            "AttachStdout": false,
>            "AttachStderr": false,
>            "ExposedPorts": {
>                "3306/tcp": {},
>                "33060/tcp": {}
>            },
>            "Tty": false,
>            "OpenStdin": false,
>            "StdinOnce": false,
>            "Env": [
>                "MYSQL_DATABASE=diamant",
>                "MYSQL_USER=diamant",
>                "MYSQL_PASSWORD=diamant",
>                "MYSQL_ROOT_PASSWORD=diamant",
>                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
>            ],
>            "Cmd": [
>                "mysqld"
>            ],
>            "Healthcheck": {
>                "Test": [
>                    "CMD-SHELL",
>                    "/healthcheck.sh"
>                ]
>            },
>            "Image": "mysql/mysql-server:8.0.21",
>            "Volumes": {
>                "/var/lib/mysql": {}
>            },
>            "WorkingDir": "",
>            "Entrypoint": [
>                "/entrypoint.sh"
>            ],
>            "OnBuild": null,
>            "Labels": {
                >"com.docker.compose.config-hash": "26a28b95600cac9d288f7aae731f956d2154ebaee9866fa9e8977821c88db3bf",
>                "com.docker.compose.container-number": "1",
>                "com.docker.compose.oneoff": "False",
>                "com.docker.compose.project": "mysql",
>                "com.docker.compose.project.config_files": "docker-compose.yml",
                >"com.docker.compose.project.working_dir": "/Users/gvalamatsas/Documents/production/koula/qa-engineers/Staging Environments/dashboard-qa.omilia.com/DiaManT/Databases/MySQL",
>                "com.docker.compose.service": "mysql_8_0_21",
>                "com.docker.compose.version": "1.27.4"
>            }
>        },
>        "NetworkSettings": {
>            "Bridge": "",
>            "SandboxID": "96e876d713128911d44d60d9a1f7990f04ebdfbd6dfad86081607403f5fea42f",
>            "HairpinMode": false,
>            "LinkLocalIPv6Address": "",
>            "LinkLocalIPv6PrefixLen": 0,
>            "Ports": {
>                "3306/tcp": [
>                    {
>                        "HostIp": "0.0.0.0",
>                        "HostPort": "3308"
>                    }
>                ],
>                "33060/tcp": null
>            },
>            "SandboxKey": "/var/run/docker/netns/96e876d71312",
>            "SecondaryIPAddresses": null,
>            "SecondaryIPv6Addresses": null,
>            "EndpointID": "",
>            "Gateway": "",
>            "GlobalIPv6Address": "",
>            "GlobalIPv6PrefixLen": 0,
>            "IPAddress": "",
>            "IPPrefixLen": 0,
>            "IPv6Gateway": "",
>            "MacAddress": "",
>            "Networks": {
>                "mysql_default": {
>                    "IPAMConfig": null,
>                    "Links": null,
>                    "Aliases": [
>                        "mysql_8_0_21",
>                        "f28e9dc04359"
>                    ],
>                    "NetworkID": "00088c79570b0e1b3863ebd7188718f42ce822a524d120a1caf7256e83a9124d",
>                    "EndpointID": "7ce9aab4238d75ca80c2410fafdef8e9de7cc251dc964ad990c7765680807ee7",
>                    "Gateway": "172.23.0.1",
>                    "IPAddress": "172.23.0.2",
>                    "IPPrefixLen": 16,
>                    "IPv6Gateway": "",
>                    "GlobalIPv6Address": "",
>                    "GlobalIPv6PrefixLen": 0,
>                    "MacAddress": "02:42:ac:17:00:02",
>                    "DriverOpts": null
>                }
>            }
>        }
>    }
>]
>```
></details>
>
><br/>

---
`docker container stats`<br/>
Shows live performance data for all containers.

>**Example:**
>
>`docker container stats`
>
> Example output:
>```console
>CONTAINER ID        NAME                   CPU %               MEM USAGE / LIMIT     MEM %               NET I/O             BLOCK I/O           PIDS
>f28e9dc04359        mysql_mysql_8_0_21_1   2.71%               435.3MiB / 1.941GiB   21.90%              172MB / 157MB       7.82MB / 272MB      112
>77884e4ff232        mysql_mysql_5_7_32_1   0.28%               249.6MiB / 1.941GiB   12.56%              180MB / 182MB       1.93MB / 147MB      100
>```
>
>**Note 1:** Add the option `--help` to see more options.</br>
>**Note 2:** `CTRL + C` to exit the view.</br>
><br/>