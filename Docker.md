# Docker

## Running a image with Docker

`$ docker run <image>:<tag>`

## Running a Hello world container with Docker

`$ docker run busybox echo "Hello World`

##### Result

```
Unable to find image 'busybox:latest' locally
latest: Pulling from library/busybox
91f30d776fb2: Pull complete
Digest: sha256:9ddee63a712cea977267342e8750ecbc60d3aab25f04ceacfa795e6fce341793
Status: Downloaded newer image for busybox:latest
Hello World
```

## A simple Node.js app: app.js

```
const http = require('http');
const os = require('os');
console.log("Kubia server starting...");
var handler = function(request, response) {
console.log("Received request from " + request.connection.remoteAddress);
response.writeHead(200);
response.end("You've hit " + os.hostname() + "\n");
};
var www = http.createServer(handler);
www.listen(8080);
```

## Creating a Dockerfile for the image

```
FROM node:7
ADD app.js /app.js
ENTRYPOINT ["node", "app.js"]
```

## Building the container image

`$ docker build -t kubia .`

##### Result

```
Sending build context to Docker daemon  60.42kB
Step 1/3 : FROM node:7
 ---> d9aed20b68a4
Step 2/3 : ADD app.js /app.js
 ---> Using cache
 ---> b7009e1e81da
Step 3/3 : ENTRYPOINT ["node", "app.js"]
 ---> Using cache
 ---> aa8beba87560
Successfully built aa8beba87560
Successfully tagged kubia:latest
```

## Listing locally stored images

`$ docker images`

```
REPOSITORY                           TAG                 IMAGE ID            CREATED             SIZE
kubia                                latest              aa8beba87560        18 minutes ago      660MB
```

## Running the container image

`$ docker run --name kubia-container -p 8080:8080 -d kubia`

#### Result

`0c84657a9115d659384b0509a94907517b1c1f15e8734476ba06ce677c029c3f`

## Checking on localhost

`$ curl localhost:8080`

#### Result

`You've hit 0c84657a9115`

## Listing running containers

`$ docker ps`

#### Result

```
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS              PORTS                    NAMES
0c84657a9115        kubia               "node app.js"       About a minute ago   Up About a minute   0.0.0.0:8080->8080/tcp   kubia-container
```

## Getting Additional Information About Container

`$ docker inspect kubia-container`

#### Result

```
[
    {
        "Id": "0c84657a9115d659384b0509a94907517b1c1f15e8734476ba06ce677c029c3f",
        "Created": "2020-07-01T12:11:14.376517222Z",
        "Path": "node",
        "Args": [
            "app.js"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 2250,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2020-07-01T12:11:14.705728871Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:aa8beba87560f8860688d62c54cca4049f23e0f08b347d278300f453e80ba78e",
        "ResolvConfPath": "/var/lib/docker/containers/0c84657a9115d659384b0509a94907517b1c1f15e8734476ba06ce677c029c3f/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/0c84657a9115d659384b0509a94907517b1c1f15e8734476ba06ce677c029c3f/hostname",
        "HostsPath": "/var/lib/docker/containers/0c84657a9115d659384b0509a94907517b1c1f15e8734476ba06ce677c029c3f/hosts",
        "LogPath": "/var/lib/docker/containers/0c84657a9115d659384b0509a94907517b1c1f15e8734476ba06ce677c029c3f/0c84657a9115d659384b0509a94907517b1c1f15e8734476ba06ce677c029c3f-json.log",
        "Name": "/kubia-container",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {
                "8080/tcp": [
                    {
                        "HostIp": "",
                        "HostPort": "8080"
                    }
                ]
            },
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "Capabilities": null,
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/b236a6aa15a54f4a3d98f19b89ffaf4f0a0762bee808302e58d9950c98677176-init/diff:/var/lib/docker/overlay2/4c05b51042b2a495133b00aa393450e16919c99c89c3ad1aa83cc5af7fc7e9c7/diff:/var/lib/docker/overlay2/b0fe6bfcf985257549a3cb5f0961f671cde4ff342d61a45ca372b832cef43e24/diff:/var/lib/docker/overlay2/c5c30b567732c272e288900024cd93a2249a8c6b1458839242642647cf47ddd9/diff:/var/lib/docker/overlay2/145894b5b3c3d708d50fbb3e07c3220846b5d0a146e04c64cccc7246a882b798/diff:/var/lib/docker/overlay2/4a20f40a2caf55f87142a025089763719066c5cc7d1d2d6919a9e6b5db9b7c8c/diff:/var/lib/docker/overlay2/e80b8f6f7a1c7e05ce342ee839dd62b60f6a782178f8265b103905edadd8dd1a/diff:/var/lib/docker/overlay2/05704a1f49e72e75c2299335d4c306e211350f60ed577b2d0e1e7d7229559c4e/diff:/var/lib/docker/overlay2/a3759c93440eb8a1c3fa7f31b345c8e89d8095a86da46c6cc28daf69f26bf4b1/diff:/var/lib/docker/overlay2/871a05d0df072a0afe118e2a82333bc4d12600a5771c5607062b656d90b24fac/diff",
                "MergedDir": "/var/lib/docker/overlay2/b236a6aa15a54f4a3d98f19b89ffaf4f0a0762bee808302e58d9950c98677176/merged",
                "UpperDir": "/var/lib/docker/overlay2/b236a6aa15a54f4a3d98f19b89ffaf4f0a0762bee808302e58d9950c98677176/diff",
                "WorkDir": "/var/lib/docker/overlay2/b236a6aa15a54f4a3d98f19b89ffaf4f0a0762bee808302e58d9950c98677176/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "0c84657a9115",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "8080/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NPM_CONFIG_LOGLEVEL=info",
                "NODE_VERSION=7.10.1",
                "YARN_VERSION=0.24.4"
            ],
            "Cmd": null,
            "Image": "kubia",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": [
                "node",
                "app.js"
            ],
            "OnBuild": null,
            "Labels": {}
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "fd24ae52727749d5c7c773b1890bd6c599f71958bf46d863985614d2b0c51fc1",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {
                "8080/tcp": [
                    {
                        "HostIp": "0.0.0.0",
                        "HostPort": "8080"
                    }
                ]
            },
            "SandboxKey": "/var/run/docker/netns/fd24ae527277",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "2cabbb0c4a2a1b3341cdad41576b14a3e7f391f6d3b11fe1d355f3b807a6c527",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "6ab83698efb5d9ba5313390d3346a4d6b5d3dbabc5ac6ed97ec71f6f314230d1",
                    "EndpointID": "2cabbb0c4a2a1b3341cdad41576b14a3e7f391f6d3b11fe1d355f3b807a6c527",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:02",
                    "DriverOpts": null
                }
            }
        }
    }
]
```

## RUNNING A SHELL INSIDE AN EXISTING CONTAINER

`$ docker exec -it kubia-container bash`

#### Result

```
root@0c84657a9115:/#
```

## Listing processes from inside a container

`$ ps aux`

#### Result

```
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  1.3 614436 26584 ?        Ssl  12:11   0:00 node app.js
root        13  0.0  0.1  20248  3072 pts/0    Ss   12:20   0:00 bash
root        18  0.0  0.1  17504  2052 pts/0    R+   12:23   0:00 ps aux
```

## A container has its own complete filesystem

`$ ls`

#### Result

```
app.js  boot  etc   lib    media  opt   root  sbin  sys  usr
bin     dev   home  lib64  mnt    proc  run   srv   tmp  var
```

## Exiting from running container

`$ exit`

#### Result

`exit`

## Stopping a container

`$ docker stop kubia-container`

#### Result

`kubia-container`

### Checking the processes

`$ docker ps -a`

#### Result

```
CONTAINER ID        IMAGE                                COMMAND                  CREATED             STATUS                            PORTS                    NAMES
0c84657a9115        kubia                                "node app.js"            22 minutes ago      Exited (137) About a minute ago                            kubia-container
```

## Removing a container

`$ docker rm kubia-container`

#### Result

`kubia-container`

## TAGGING AN IMAGE UNDER AN ADDITIONAL TAG

`$ docker tag kubia adnanasghar/kubia`

## A container image can have multiple tags

`$ docker images | head`

#### Result

```
REPOSITORY                           TAG                 IMAGE ID            CREATED             SIZE
adnanasghar/kubia                    latest              aa8beba87560        53 minutes ago      660MB
kubia                                latest              aa8beba87560        53 minutes ago      660MB
busybox                              latest              c7c37e472d31        40 hours ago        1.22MB

```

## PUSHING THE IMAGE TO DOCKER HUB

`$ docker push adnanasghar/kubia`

#### Result

````
The push refers to repository [docker.io/adnanasghar/kubia]
dd8ff4c19087: Pushed
ab90d83fa34a: Mounted from library/node
8ee318e54723: Mounted from library/node
e6695624484e: Pushed
da59b99bbd3b: Mounted from library/node
5616a6292c16: Mounted from library/node
f3ed6cb59ab0: Mounted from library/node
654f45ecb7e3: Mounted from library/node
2c40c66f7667: Mounted from library/node
latest: digest: sha256:18f47e1554daae84617004c7acd53d1600b519bb7aa4db7416ecc9a1b5c80f98 size: 2213```
````

## RUNNING THE IMAGE ON A DIFFERENT MACHINE

`$ docker run -p 8080:8080 -d adnanasghar/kubia`

#### Result

```
1f859af3742897272be57c118d67b8335f12f842a3bd62fc119102b5699a25c2
```
