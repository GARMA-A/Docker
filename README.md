# Docker most used Commands


##docker
```sh
$docker --version
$docker info

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

#Stop a running container
$ docker container stop <containername>

#Start a stopped container
$ docker container start <containername>

#Delete a stopped container
$ docker container rm <containername>
$ docker container run -d -p 8080:80 nginx:latest

```







