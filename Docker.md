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
busybox                              latest              c7c37e472d31        40 hours ago        1.22MB
adnanasghar/node-app-image           latest              d0cf8a2d16fc        3 weeks ago         58.8MB
node-app-image                       latest              d0cf8a2d16fc        3 weeks ago         58.8MB
first-docker-app                     latest              aadd730ee76a        3 weeks ago         132MB
web                                  latest              b16c143541d9        3 weeks ago         82.4MB
nginx                                latest              4392e5dad77d        4 weeks ago         132MB
test                                 latest              df058402d75d        4 weeks ago         82.4MB
alpine                               latest              a24bb4013296        4 weeks ago         5.57MB
ubuntu                               latest              1d622ef86b13        2 months ago        73.9MB
nigelpoulton/pluralsight-docker-ci   latest              dd7a37fe7c1e        5 months ago        604MB
aamirpinger/helloworld               latest              29388024b9db        17 months ago       109MB
```
