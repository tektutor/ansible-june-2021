### Docker Commands

#### Finding the docker version
```
docker --version
```

#### Finding details about docker installation
```
docker info
```

#### Listing docker images from Local Docker Registry
```
docker images
```

#### Deleting an image from Local Docker Registry
```
docker rmi hello-world:latest
```

#### Downloading an image from Docker Hub to Local Docker Registry
```
docker pull ubuntu:16.04
```

#### Creating our first docker container
```
docker run hello-world:latest
```
#### Creating a container in foreground(interactive) mode
```
docker run -it --name ubuntu1 --hostname ubuntu1 ubuntu:18.04 /bin/bash
```

#### Creating a container in background(deattached/daemon) mode
```
docker run -dit --name ubuntu2 --hostname ubuntu2 ubuntu:18.04 /bin/bash
```

#### Opening a shell inside a running container
```
docker exec -it ubuntu2 /bin/bash
```

#### Listing the currently running docker containers 
```
docker ps
```

#### Listing all containers including exited ones
```
docker ps -a
```

#### Listing all currently running container ids
```
docker pa -q
```

#### Listing all containers id including exited ones
```
docker ps -aq
```

#### Stopping a running container
```
docker stop ubuntu1
```

#### Starting a stopped container
```
docker start ubuntu1
```

#### Restarting already created container
```
docker restart ubuntu1
```

#### Deleting a running container graciously
```
docker stop ubuntu1 && docker rm ubuntu1
```

#### Deleting a running container abruptly
```
docker rm -f ubuntu1
```

#### Finding IP address of a container
```
docker inspect ubuntu1 | grep IPA
docker inspect -f {{.NetworkSettings.IPAddress}} ubuntu1
```
#### Creating a custom Docker ubuntu image with vim tree git installed
You need to create a Dockerfile as shown below
```
FROM ubuntu:18.04
MAINTAINER Jeganathan Swaminathan <jegan@tektutor.org>

RUN apt-get update && apt-get install -y git vim tree
```

You may now build your custom image as shown below
```
docker build -t tektutor/custom-ubuntu .
```

You may verify if your custom docker images is in local docker registry
```
docker images
```


