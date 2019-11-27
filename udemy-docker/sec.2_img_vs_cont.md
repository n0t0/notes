### Image vs. Container

- image is the application we want to run
- container is an instance of that image running as a process 
- many containers can run of the same image 

$ docker container run --publish 80:80 nginx 
$ docker container run --publish 80:80 --detach nginx --> run it on bg
$ docker container ls --> list containers 

$ docker container stop <con id(first unique digits)>

$ docker container run --publish 80:80 --detach --name webhost nginx

$ docker container logs webhost --> spin logs for 
$ docker container top <container> --> list processes 

### Removing Containers 

$ docker container rm [<con id1>, <con id2>, <con id3>,...]
$ docker container rm -f --> remove running container  
$ docker stop $(docker ps -q) --> stop running containers
$ docker stop $(docker ps -a -q) --> stop all containers

### What docker container run Does

1. looks for a local image 
2. pull from Docker Hub if not finded locally
3. downloads the latest version - (nginx:latest by default)
4. creates container 
5. gives it a virtual IP on a private network 
6. opens up port 80 on host and forwards port 80 in container 
7. starts container by using the CMD in the image Dockerfile 

$ docker container run -p 8080:80 --name webhost -d nginx:1.11 nginx -T

$ docker container run -e MYSQL_RANDOM_ROOT_PASSWORD=true --publish 3306:3306 --name db -d mysql

--env VARIABLE=x

### Container Monitoring 

$ docker container top <container>
$ docker container inspect <container>
$ docker container stats --> CTRL + C to quit 
$ docker container --filter status=dead
$ docker container --filter health=healthy


### Getting Inside a Container 

$ docker container run -it --> start new container interactively 
$ docker container exec -it --> run additional command in existing container 

$ docker container run -it --name proxy nginx bash
$ docker container run -it --rm <container> --> remove container afte exit 


$ docker container start -ai <container> --> attach to an existing container (helpful to see logs)
$ docker container exec -it <container> bash --> get to an existign container

- alpine is designed to be small and therefore uses sh, not bash

$ docker container run -it alpine sh
$ dk run --entrypoint /bin/bash <container>