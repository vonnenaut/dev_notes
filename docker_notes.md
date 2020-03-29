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





