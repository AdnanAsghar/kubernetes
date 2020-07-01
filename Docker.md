# Docker

## Running a image with Docker
```$ docker run <image>:<tag>```
  
## Running a Hello world container with Docker
```$ docker run busybox echo "Hello World```

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
```$ docker build -t kubia .```

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
