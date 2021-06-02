### Docker Commands

#### Installing Docker
```
sudo yum install -y yum-utils
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install -y docker-ce
sudo systemctl enable docker && sudo systemctl start docker
```

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

#### Finding details of an image
```
docker image inspect ubuntu:18.04
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

#### Volume Mounting - persisting data outside container
```
docker run -d --name mysql1 --hostname mysql1 -v /tmp/mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root mysql:latest
```

Try getting inside the mysql1 container
```
docker exec -it mysql1 bash
```

Try to connect to the mysql server, when prompted for password type 'root'
```
mysql -u root -p
```

Try creating database, table and few records into the table
```
CREATE DATABASE tektutor;
USE tektutor;
CREATE TABLE training ( id INT, name VARCHAR(25), duration VARCHAR(25 ) );
INSERT INTO training VALUES ( 1, "DevOps", "5 Days" );
INSERT INTO training VALUES ( 2, "Kubernetes", "5 Days" );
INSERT INTO training VALUES ( 3, "Ansible", "5 Days" );
```

Now comeout of mysql1 container and delete the mysql1 container
```
exit
exit
docker rm -f mysql1
```

Recreate a new container as shown below
```
docker run -d --name mysql2 --hostname mysql2 -v /tmp/mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root mysql:latest
```

Get inside the new container, you should be able to see the tektutor and training table and its data intact.
```
docker exec -it mysql2 bash 
mysql -u root -p
SHOW DATABASES;
USE tektutor;
SELECT * FROM training;
```
