This file contains the most common commands used in Docker.

$ docker pull busybox
    pulls a container called 'busybox' 

$ docker images
    shows all the images

$ docker run busybox
    run the docker container

$ docker run busybox echo "hello from busybox"
    runs a command as well inside the container

$ docker ps
    shows all containers that are currently running

$ docker ps -a
    shows all containers

$ docker run -it busybox sh
/ # ls
bin   dev   etc   home  proc  root  sys   tmp   usr   var
/ # uptime
 05:45:21 up  5:58,  0 users,  load average: 0.00, 0.01, 0.04
    
    runs more than one command at a time
    -it : interactive

$ docker rm 305297d7a235 ff0a5c3750b9
    remove containers

$ docker rm $(docker ps -a -q -f status=exited)
    deletes all containers having exited status
    -f : filter
    -q : numeric id

$ docker container prune
    does the same : removes containers

$ docker run -d -P --name static-site prakhar1989/static-site
    -d : detached mode - detaches the terminal
    -P : publish all exposed ports to random ports
    --name : the name we want ot give

$ docker port static-site
    to get the port in which the container is running

$ docker run -p 8888:80 prakhar1989/static-site
    to specify port to which client will forward connections to the container

$ docker stop static-site
    to stop detached container

$ docker images
    show all images in local

$ docker build -t prakhar1989/catnip .
    building an image
    -t  : tag

$ docker run -p 8888:5000 prakhar1989/catnip
    running it -> port 5000 for server inside -> exposed on port 8888

$ docker login
    login using dockerHUb creds

$ docker push prakhar1989/catnip
    pushing to dockerhub

$ docker search elasticsearch
    searches docker hub for elasticsearch 
    pull elasticsearch from registry listed in 'https://www.docker.elastic.co/'. They maintain official images

$ docker run -d --name es -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:6.3.2
    --name  :  name for the container. Here, it is es
    -d      :  detach = true
    -p      :  --publish <[hostPort:]containerPort>
                Publish a container's port, or range of ports, to the host.4
    -e,---env   :  set environment variables

$ docker run -d --name es --net foodtrucks-net -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:6.3.2
    --net   : to specify which network to run on

$ docker run -it --rm skoolguyajmal/foodtrucks-web bash
    -it :  interactive mode
    bash:   with bash process
    
$ docker container logs <container name>
    shows the logs



____________________________________________________________________________________________________________________________________________
DOCKER NETWORK
--------------

$ docker network ls
    lists all networks created by docker

$ docker network inspect bridge
    inspects the specified network.Here, it is the bridge

$ docker network create foodtrucks-net
    creates a bridge network called foodtrucks-net

___________________________________________________________________________________________________________________________________________
Get the whole thing running by:

$ git clone https://github.com/prakhar1989/FoodTrucks
$ cd FoodTrucks
$ ./setup-docker.sh
