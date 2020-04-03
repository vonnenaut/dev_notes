# Docker Notes

Docker is for running application environments inside containers, somewhat like VMs, but more dependent on the OS and more lightweight and flexible.

Traversy Media 'Exploring Docker [1] - Getting Started':

https://www.youtube.com/watch?v=Kyx2PsuwomE&t=503s



## Installation

https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04



## Usage

`docker [option] [command] [arguments]`

`docker docker-subcommand --help`

`docker version`

`docker info`



**Example:  Publish an Nginx server container**

`docker container run -it -p 80:80 nginx`

​	Create a container interactively (as opposed to in the background) (-it) and publish it (-p) on local machine port 80 (80:) using the container's port 80 (80), using nginx web server.  The first 80 could be anything in terms of your local ports but the second should be 80 for nginx.



`docker container ls`

shows running containers



`docker container ls -a`

shows all containers on system (running or not)	



`docker container rm [first few letters of container ID]

removes/deletes the specified container



`docker images`

lists all images on the local system



docker image rm [first three chars of image ID]

delete the local copy of the specified image



`docker pull [image name]`

download the specified image



`docker container run -d -p 8080:80 --name mynginx nginx`

start a container named mynginx with nginx running in it on local port 8080 with nginx's exposed port 80 and do this in the background, detached (-d)



`docker ps` or `docker container ps`

an older way to show containers (add -a to also show those not running)



`docker container run -d -p 8081:80 --name myapache httpd`

start a container in detached mode running Apache on localhost's port 8081 with Apache listening on its own port 80 (httpd is the name of the Docker container for Apache web server)



```
Go to Dockerhub and search for containers to get their official names.

https://hub.docker.com/
```



`docker container run -d -p 3306:3306 --name mysql --env MYSQL_ROOT_PASSWORD=123456 mysql

start a container running mysql database on localhost port 3306 using mysql's port 3306, setting the root password as 123456



`docker container rm myapache -f`

force-remove a running container





## How to Edit Files in a Container:  Volumes and Bind Mounts

`$ docker container exec -it mynginx bash`

bash into container, accessing its filesystem interactively (-it)













