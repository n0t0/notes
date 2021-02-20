#### Docker Demo

"""
In development, Docker allows keeping the whole infrastructure as a code and sharing it with others in your team. Do you know dialogues like this?

you: "Hey Chris, my development application won't start. Have you changed something?"

chris: "Oh yes, I forgot to tell. We have new database engine now. Also, you need to install redis, and drivers for it. It's very easy, take a look into docs and you'll do it in few moments."

Of course, it always takes more time. If you work in a bigger team, such situations can happen more often and are harder to spot. With Docker, to sync with changes you need to just run docker-compose up --build, and after few moments new version of the development stack will be running, no matter what changed. Moreover, introducing new developer to the project will look exactly the same! Imagine how much time it can save?
"""

- 12 factor -

### Getting Started

- image: an executable package
- container: a runtime instance of an image

### Containers vs Virtual Machines

- container shares the kernel of the host with containers
- VM runs a full-blown 'guest' OS with virtual acess to host resources

### Linux Distribution

- docker is kernel and storage driver dependent

## Containers

### Dockerfile

- Dockerfile defines what goes on in the env inside the container
- Dockerfile doesn't have to be inside the directory it can be passed with -f when building the image
- same for other context data

### requirements.txt

- requirenments.txt and app.py go in directory with Dockerfile

#### Build Custom Image

- Dockerfile

FROM --> base OS layer

$ docker build -t <image:tag> .
$ docker build -f </path/to/App.Dockerfile> -t <image:tag> .

- images are immutable
- container appears to be a copy of the image but is a link; if there is a change to a file/directory on the filesystem; its copied up to write/read layer

#### Tag and Push and Pull

$ docker login --> stores a session ID
$ docker logout --> from untrusted host

$ docker image tag <image> <name/image>
$ docker image tag <image:latest> <docker.ambrygen.com/namespace/image:latest>

- global namespace is only writable by administrators

$ docker push <docker.ambrygen.com/namespace/image:latest>
$ docker pull <docker.ambrygen.com/namespace/image:latest>


$ docker run -d -p 5000:5000 --restart always --name registry registry:2
$ docker build . -t <name/app>
$ docker push localhost:5000/<name/app>


#### Run, Stop and Remove a Container/s

$ docker container run --publish 80:80 nginx
$ docker container run -d -p 80:80 nginx

$ docker container stop <ID>

$ docker container rm <ID>

#### Jump onto a Container

$ docker container exec -it <container> bash
$ docker exec -it <container> bash -c 'tree -a /tmp'
$ dk run --entrypoint /bin/bash <container> --> overwrite ENTRYPOINT
$ dk ps -s --> container size on disk

#### Copy from/to container

$ docker cp script.sh <container>:/tmp/
$ docker cp <container>:/tmp/. .

#### Logging

$ docker logs -f <someread>
$ docker logs --tail 10 <someread>
$ docker logs -h

#### Monitoring

- displaying asc size and image tag

$ curl -s --unix-socket /var/run/docker.sock http:/images/json | jq '.[] | "\(.Size) \(.RepoTags[])"' test.json | sort -V

- rm -rf *

$ docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <container> --> container IP

$ docker system prune -a --volumes

#### Manage Stack of Containers

- settings like commands, ports, volumes, variables, networks etc are taken from docker-compose.yml

$ docker-compose up --build
- --build recheck if image already exists
$ doker-compose up -p <projectName> -d

#### Volumes/Mounts

- volumes can be shared among multiple containers
- replicas having access to the same files (NFS driver)
- --volumes-from --> create a container that mounts that volume

$ docker run --rm --volumes-from dbstore -v $(pwd):/backup ubuntu tar cvf /backup/backup.tar /dbdata --> backup data

- anonymous volumes are deleted when vs named volumes

$ docker run --rm -v /foo -v awesome:/bar busybox top --> foo is deleted but not awesome volume

$ docker volume create --driver local \
 - opt type=none \
 - opt device=/var/opt/my_website/dist \
 - opt o=bind web_data

#### Mount

 $ docker run -d \
  --name devtest \
  --mount source=myvol2,target=/app \
  nginx:latest

$ docker service create \
     --mount 'type=volume,src=<VOLUME-NAME>,dst=<CONTAINER-PATH>,volume-driver=local,volume-opt=type=nfs,volume-opt=device=<nfs-server>:<nfs-path>,"volume-opt=o=addr=<nfs-address>,vers=4,soft,timeo=180,bg,tcp,rw"'
    --name myservice \
    <image>


#### Populate a Volume Using a Container

$ docker run -d \
  --name=nginxtest \
  --mount source=nginx-vol,destination=/usr/share/nginx/html \
  nginx:latest

#### Volume Drivers

$ docker plugin install --grant-all-permissions vieux/sshfs

$ docker volume create --driver vieux/sshfs \
  -o sshcmd=test@node2:/home/test \
  -o password=testpassword \
  sshvolume

$ docker run -it --rm \
    --mount type=volume,dst=/container/path,volume-driver=local,volume-opt=type=nfs,\"volume-opt=o=nfsvers=4,addr=192.168.1.1\",volume-opt=device=:/host/path \
    foo

#### Start a Container With a Volume Driver

$ docker run -d \
  --name sshfs-container \
  --volume-driver vieux/sshfs \
  --mount src=sshvolume,target=/app,volume-opt=sshcmd=test@node2:/home/test,volume-opt=password=testpassword \
  nginx:latest


#### Backup, Restore, Migrate Data Volumes

- --volume-from

#### Healthcheck

HEALTHCHECK --interval=5s --timeout=10s --retries=3 CMD curl -sS 127.0.0.1:8080 || exit 1


#### Run/Deploy (registry)

$ docker stack deploy -c <stack-file.yml> <projectName>

#### Network

$ docker network ls

$ docker run ubuntu
$ docker run ubuntu --network=none
$ docker run ubuntu --network=host

$ docker network create --driver overlay --subnet 10.0.9.0/24 my-overlay-network
$ docker service create --replicas 2 --network my-overlay-network nginx

- embedded DNS --> reference by container name, not IP

### Quorum

- minimum number of votes that a consensus group needs in order to be allowed to perform an operation
- (N/2) + 1 --> 7/2 = 3 + 1 = 4 --> quorum
- odd numbers

## Swarms

- swarm a group of machines running Docker and joined into a cluster

- emptiest node fills the least utilized machine with containers
- global each node gets exactly one instance of specified container

- only swarm managers authorize machines to join the swarm as workers

- when swarm mode is on - docker executes commands on the swarm not only local machine

### Raft 

- log replication 
- leader election 
- safety 

- not running work on managers nodes

$ docker node update --availability drain <NODE>

### Leader Election & Log Replication 

- leader goes down, first follower to timeout send an election 

#### Multi-node Swarm/Scaling/Orchestration/Management 

- load balancing
- highly available 
- scaling
- rolling updates (little to none down-time when deploying)
- secure
- self-healing
 
#### Swarm Management 

$ docker node update --label-add <key>=<value> <node-id> --> label a node 
$ docker service create --constraint 'node.labels.type == webserver' nginx
$ docker service create --name redis --placement-pref 'spread=node.labels.dc' redis

$ docker node inspect self --pretty
$ docker node update --availability drain <node>

### Services

- replicated and global services

$ docker service create --replicas=3 my-web-server
$ docker service create --mode global my-monitoring-agent

$ docker service update --replicas=4 my-web-server

#### Rolling Updates

$ docker service update --image redis:3.0.7 redis
$ docker service update --help

#### Secrets 

$ docker secret create <secret_name> <local_secret_file.txt>
$ echo "strong_password" | docker sercret create <secret_name> -

$ docker service create --name psql --secret psql_user --secret psql_pass -e POSTGRES_PASSWORD_FILE=/run/secrets/psql_pass -e POSTGRES_PASSWORD_FILE=/run/secrets/psql_user postgres

$ docker service update \
  --secret-rm secret-1 \
  --secret-add src=secret-2,target=db-password \r
  web

#### Kubernetes 

#### Backup and Restore 

- choose your one of your container
$ docker ps -a
$ docker commit -p <container> <backupName>
- it will appear one image with <YOUR_BACKUP_NAME>
$ docker images

- save docker container to archive

$ docker save -o <container>.tar <backupName>

- restore container 

$ docker load -i <CONTAINER_FILE>.tar

#### Docker Cloud

www.cloud.docker.com

- link Cloud Providers --> AWS
- link Source Providers --> BitBucket


#### Networking - Kubernetis 

- Calico
- Tigera
- Weaveworks
- flannel

### vMotion or DRS (scheduler)

- 