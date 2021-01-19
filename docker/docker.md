### Docker Version

$ docker --version
$ docker info --> more info
- how many containers
- how many containers are running or stopped
$ docker version --> more info
$ docker 2x TAB
$ docker image 2 TAB
$ docker --> list of commands

### Docker Installation

$ curl -sSL https://get.docker.com/ | sh

$ curl -fsSL get.docker.com -o get-docker.sh
$ sh get-docker.sh

https://docs.docker.com/machine/install-machine/#install-bash-completion-scripts
https://github.com/docker/machine/releases --> docker-machine
https://github.com/docker/compose/releases --> docker-compose

$ docker image ls --> list images
$ docker container ls --all --> list containers

### Create and Remove Container Image

- from top level directory

$ docker build -t friendlyhello:<v1> . --> -t (tag) build an image
$ docker image ls  --> lists the built image
$ docker images -a

$ docker image history <img> --> check layers

$ docker rmi $(docker images -q)

### Run Container

$ docker run -p 4000:80 friendlyhello
$ docker run -d -p 4000:80 friendlyhello --> runs in the background, detached mode
$ docker container run -rm -it ubuntu:14.04 bash --> remove container after exit
g
$ docker start <container>
$ docker attach <container> --> attach to a container CTRL-P; CTRL-Q --> detach

$ docker run -dit --name <name> busybox

#### by default all containers are runned by root

$ docker run -d --user 1001 ubuntu:latest sleep --> run container as UID

### Stop and Remove Container

$ docker container ls --> get container ID
$ docker ps -a
$ docker stop $(docker ps -a -q) --> stop all containers
$ docker rm $(docker ps -a -q) --> remove all containers
$ docker container stop <ID>

## Services (Share/Publish Image )

$ docker login --> sign up first cloud.docker.com

### Tag the Image

- username/repository:tag

$ docker tag image username/repo:tag
$ docker tag friendlyhello maya/get-started:part2

$ docker image ls

### Publish the Image

$ docker push username/repository:tag

$ docker run -p 4000:80 username/repository:tag --> pulling image from the repository

### Docker Compose

- define, run, and scale services with docker-compose.yml

### Load-Balancing

$ docker swarm init

$ docker stack deploy -c docker-compose.yml <appname>

$ docker service ls --> list services

$ docker service ps --> list tasks

$ docker container ls -q

### Scale the App

- change number of replicas in docker-compose.yml
- re-run:

$ docker stack deploy -c docker-compose.yml <appname>

$ docker stack rm <appname> --> take down the app
$ docker swarm leave --force -->  take down the swarm

## RUN, ENTRYPOINT, CMD

RUN --> install dependencies; adds extra layer
ENTRYPOINT --> ["/bin/echo", "Hello"]
CMD --> ["World"]

### Set-up Swarm

$ docker swarm init
$ docker swarm join

### Scheduling

$ docker service create --constraints 'node.labels.type=web' my-app --> hard

$ docker node update --label-add datacenter=a node1
$ docker node update --label-add datacenter=a node2
$ docker node update --label-add datacenter=z node3

$ docker service create --name redis --replicas 12 --placement-pref 'spread=node.labels.dc' redis

### Failure Recovery - Losing Quorum

$ docker swarm init --force-new-cluster --> on a healthy manager; then promote managers

### Restore From a Backup

$ systemctl stop docker
$ sudo rm -rf /var/lib/docker/swarm
$ cp -a back.up /var/lib/docker/swarm/
$ systemctl start docker
$ docker swarm init (--force-new-cluster)

## Volumes

- tmpfs mounts for non-persistent state data

### -v or --mount flag

- -v or --volume consists of three fields speareted by :
1. name of the volume and is unique
2. path where file or directory are mounted in the container
3. optional options such as **ro**

- --mount consists of key-value tuples separated by ,
1. _type_ of the mount: _bind_, _volume_, _tmpfs_
2. _source_ of the mount; the name of the volume
3. _destination_ takes as its value the path where the file or directory is mounted in the container
4. _readonly_ option
5. _volume-opt_

### Create and Manage Volumes

$ docker volume create my-vol --> creates a volume
$ docker volume ls --> list volumes
$ docker volume inspect my-vol --> inspect a volume
$ docker volume rm my-vol

### Start a Container with a Volume (that does not yet exist)

$ docker run -d \
  --name devtest \
  --mount surce=volume_02,target=/app \
  nginx:latest

$ docker inspect devtest

### Start a Service with a Volumes

$ docker service create -d \
  --replicas=4 \
  --name devtest-service \
  --mount source=volume_03,target=/app \
  nginx:latest


$ docker service ps devtest-service --> verify service is running
$ docker service rm devtest-service --> removing service stops all its tasks

### Populate a Volume Using a Container

$ docker run -d \
  --name=nginxtest \
  --mount source=nginx-volume,destination=/usr/share/nginx/html \
  nginx:latest


### read-only Volume

$ docker run -d \
  --name=nginxtest \
  --mount source=nginx-volume,destination=/usr/share/nginx/html, readonly \
  nginx:latest


### Share Data Among Machines; Ase a Volume Driver

- initial set-up for two nodes; Docker host can ssh to second host

$ docker plugin install --grant-all-permissions vieux/sshfs


### Create a Volume Using a Volume Driver

$ docker volume create --drive vieux/sshfs \
  -o sshcmd=test@node2:/home/test \
  -o password=testpassword \
  sshvolume

### Start a Container Which Creates a Volume Using a Volumde Driver

$ docker run -d \
  --name sshfs-container \
  --volume-driver vieux/sshfs \
  --mount src=sshvolume,target=/app,volume-opt=sshcmd=test@node2:/home/test,volume-opt=password=testpassword \
  nginx:latest

## Bind Mounts

$ docker run -d \
  -it \
  --name devtest \
  --mount type=bind,source="$(pwd)"/target,target=/app \
  nginx:latest

### Mounting Into a Non-empty Directory on the Container

$ docker run -d \
  -it \
  --name broken-container \
  --mount type=bind,source=/tmp,target=/usr \
  nginx:latest

**docker: Error response from daemon: oci runtime error: container_linux.go:262:
starting container process caused "exec: \"nginx\": executable file not found in $PATH".**

### Use a Read-only Bind Mount

$ docker run -d \
  -it \
  --name devtest \
  --mount type=bind,source="$(pwd)"/target,target=/app,readonly \
  nginx:latest

### Configure Bind Propagation

$ docker run -d \
  -it \
  --name devtest \
  --mount type=bind,source="$(pwd)"/target,target=/app \
  --mount type=bind,source="$(pwd)"/target,target=/app2,readonly,bind-propagation=rslave \
  nginx:latest


### Docker add Config

$ docker config create proxy-v2 nginx-v2.conf
xtd1s1g6b5zukjhvup5vi4jzd

### Docker update service

$ docker service update --config-rm proxy --config-add src=proxy-v2,target=/etc/nginx/nginx.conf proxy

### Docker update service TRAEFIK

$docker service update \
    --label-add traefik.port=8080 \
    --label-add traefik.enable=true \
    --label-add traefik.docker.network=proxy-net \
    --label-add traefik.frontend.rule=Host:<matomo-test>.ambrygen.com \
    <matomo_nginx>