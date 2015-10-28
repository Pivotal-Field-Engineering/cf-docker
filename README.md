# cf-docker
## Getting Started on Pushing Docker Images to CF
### Here is a cheat sheet on how to do it.

* First Install the Docker Toolbox on you Mac.
https://docs.docker.com/mac/step_one/
* Start the Docker Terminal from your Launchpad. This will start the docker virtual machine.
```script
TEST
  $docker run hello-world
  $docker run -it ubuntu bash
```
* Login to Docker Hub
```script
  $docker login
```
You Authentication credentials will be stored in  `~/.docker/config.json`

* Search and Pull an Image
```script
$docker search centos
$docker pull centos
$docker images
```
* Create a Repository on Docker Hub
```script
https://hub.docker.com/
```

* Create a Docker File and Build a Docker Image
[Docker Nodejs Example](https://docs.docker.com/examples/nodejs_web_app/)

```script
$docker build -t rjain15/centos-node-hello .
```

* Push it in the Repo
```script
$docker push rjain15/centos-node-hello
```
* Pull it down from Repo
```script
$docker pull rjain15/centos-node-hello
```
* Get the IP Address of you local Docker VM
```script
$docker-machine ls
NAME      ACTIVE   DRIVER       STATE     URL                         SWARM
default   *        virtualbox   Running   tcp://192.168.99.100:2376   ```

* Testing it locally
```script
$docker run -d -P --name web rjain15/centos-node-hello
$docker ps
```
* To get the Local Port Number
```script
$docker port web
8080/tcp -> 0.0.0.0:32768
curl -i http://192.168.99.100:32768
```

* Push docker image to cf
```script
cf push --docker-image rjain15/centos-node-hello -c "node /src/index.js"
Note: The start command should be same as the CMD from the Dockerfile
```

* cf apps
```script
node-first-app-docker   started           1/1         512M     1G     node-first-app-docker-beachy-playdown.west-1.fe.gopivotal.com   
```

* Test CF

```script
curl -i http://node-first-app-docker-beachy-playdown.west-1.fe.gopivotal.com
HTTP/1.1 200 OK
Content-Length: 12
Content-Type: text/html; charset=utf-8
Date: Wed, 28 Oct 2015 15:32:29 GMT
X-Cf-Requestid: 9cb1ed82-25e3-4ea0-6894-e3bd418bbf2a
X-Powered-By: Express

Hello World
```
