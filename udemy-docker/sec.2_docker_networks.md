### Concepts 

$ docker container run -p
$ docker container port <container> --> check open ports 

- by default docker connects to private virtual network "bridge"
- each virtual network routes through NAT firewall on host IP
- all containers can talk to each other without -p
- best practive is to create a new virtual network for each app:
    - my_web_app for mysql and php/apache containers 
    - my_api for mongo and nodejs containers 
- attach containers to more than one virtual network (or none)
- skip virtual networks and use host IP (--net=host)
- Docker network drivers to gain new abilities 

$ docker container inspect --format '{{ .NetworkSettings.IPAddress }}' webhost 

- cannot have two containers listening to the same port 

### Networks CLI Management 

$ docker network ls
$ docker network inspect <network>
$ docker network create --driver 
$ docker network connect 
$ docker network disconnect 

$ docker network create my_app_net
$ docker container run -d --name nginx --network my_app_net nginx --> run a container in that network 

$ docker network connect <network> <continer> --> assigns a network to a container 
$ docker network disconnect <network> <continer> 


$ docker network connect <1st container> <2nd container> --> attach a network to a container
$ docker network disconnect <1st container> <2nd container> 

### Networks DNS

$ docker container exec -it my_nginx ping new_nginx
- --link --> create a link 

### Remove Networks 

$ docker network prune 