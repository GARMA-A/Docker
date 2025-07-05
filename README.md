# Docker most used Commands


##docker
```sh
$docker --version
$docker info
$docker image history nginx:latest
$docker image inspect <image-name>:<tag>

$groups
$sudo usermod -aG docker $USER_NAME
```


##image
```sh
#List all images
$ docker image ls

#Pull the ubuntu:latest image
$ docker image pull <repository>:<tag>
$ docker image pull alpine:latest
$ docker image pull mongo:4.2.6
$ docker image pull alpine
$ docker image prune # remove all images that are not referenced by any container
$ docker image prune -a #remove all dangling images (images with no tags)

#The tag should include the repository name (your user account on Docker Hub):
$ docker image tag <current-tag> <repository-name>/<new-tag>
$ docker image tag web:latest asami76/newweb:latest
$ docker image push asami76/newweb:latest

#Dockerfile
During the `$ docker image build` and for each instruction in the Dockerfile, Docker looks to see if it already has an image layer for that instruction in its cache. If it does, this is a cache hit and it uses that layer. If it doesn’t, this is a cache miss and it builds a new layer from the instruction.

 $ docker image build -squash # not recommended to use -squash option, it will remove all the layers and create a single layer image.

```

##container
```sh
#Ctrl-PQ // will detach your shell from the terminal of a container and leave the container running (UP) in the background.
# lists all containers in the running (UP). 
#Add -a flag to list (Existed) containers
$ docker container ls 

# runs a new process inside of a running container.
$ docker container exec 

#Attach to a running container
$ docker container exec -it <containername> bash

# stop a running container and put it in the Exited (0) state.
$ docker container stop 

# will restart a stopped (Exited) container.
$docker container start 

# delete a stopped container.
$docker container rm 

# stops a running (UP) container .
$docker container stop 

# will show you detailed configuration and runtime information about a container.
$docker container inspect 

# start new containers.
$ docker container run 


#Launch a container from an image
#--i interactive mode --t terminal mode 
#/bin/bash to run a bash shell inside the container
$ docker container run -it ubuntu:latest /bin/bash
# example 
# the --name for the container is useful for replacing the id and -h for rename the 
# operating system inside the contaoner
$ docker container run -it --name "anyname" -h "anyhostname" -p 8080:80 nginx:latest /bin/bash
$ docker container run -d -p 8080:80 nginx:latest
$ curl http://localhost:8080

# full example of curl command
$ curl -X POST -H \
"Content-Type: application/json" \
-d '{"name":"John"}' https://api.example.com/users

#hadoop.asam17/hadoop-pseudo:v1.0 is the image name
# -c option to run a command inside the container
$ docker container run  hadoop.asam17/hadoop-pseudo:v1.0 bash -c "/usr/local/bootstrap.sh; bash"

# -e is to add environment variable
$docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=P@ssw0rd" -e "MSSQL_PID=Express" -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest

#Stop a running container
$ docker container stop <containername>

#Start a stopped container
$ docker container start <containername>

#Delete a stopped container
$ docker container rm <containername>
$ docker container run -d -p 8080:80 nginx:latest

```

## docker workflow

```sh
## bad workflow
# you develop you application and copy the src code into the container
$ docker cp <source-path> <container-name-or-id>:<destination-path>

# the following command copy the `test.txt` file to the container
$ docker container cp ./test.txt 7e0:/tmp/test.txt



```

## network default problems
```sh
##Example 1
$docker container run -d --name web nginx:latest
$docker container run -it --name client centos:latest
#indide centos container
$ curl http://web
#could not resolve host: web
#but if i didi the following command
$docker container inspect web
#search for ip address for example 172.17.0.2
$ping 172.17.0.2
#it works from client ping to web 

# how to make containers comunicate using names 
# first solution
$docker container run -it --name client --add-host web:172.17.0.2 centos:latest

#to show docker ip address
$ip addr show

# --network to choice a network none mean the container will not have any network
# mean it cannot send or recive any thing from host or anoher container
$docker container run --network none centos:latest

# --network host to use the host network
$docker container run --network host centos:latest

# drivers network bridge macvlan overlay for multiple hosts

```

## docker networks
```sh
# you do not need to specifiy -d bridge because bridge is the default
$ docker network create mynet -d bridge 

```







