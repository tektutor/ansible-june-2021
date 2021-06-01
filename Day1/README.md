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


