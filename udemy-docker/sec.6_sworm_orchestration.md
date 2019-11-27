### Scale Out and Scale Up 

- Protocols: 
- Raft across all the managers for internal distributed state data store
- Gossip network across workers 
- gRPC --> handles connection management 

- Push vs. Pull Models
- Heartbeat --> Kept in Leader memory 

### Replication 

- one leader manager, rest a manager followers
- managers send list of all managers' addresses to Workers

$ docker service create --> replaces docker container in swarm environment 

### Init Swarm 

$ docker swarm init 
$ docker node ls
$ docker node rm <nodeid> 
$ docker node promote <nodeid>


$ docker service = $ docker run 
$ docker service create alpine 8.8.8.8
$ docker service ls 
$ docker service ps <name>
$ docker service update <serviceName> --replicas 3 

$ docker update --help
$ dockeer service update --help

### Multi-node Swarm 

$ docker swarm init --advertise-addr <IP addr> --> accessible from other nodes 
$ docker node update --role manager <node>
$ docker swarm join-token <worker|manager>

$ docker swarm join --token <token>

$ docker swarm --force-new-cluster --advertise-addr 

$ docker service create --replicas 3 alpine 8.8.8.8  
$ docker service ps <node> --> list containers running on that node 
$ docker service ps <service> --> full service list 

### docker-machine

$ docker-machine create -h
$ docker-machine ssh <machinename>

### Multi-Host 

$ docker network create --drive overlay <networkname>

$ docker service create --name psql --network gpu_dmz -e POSTGRES_PASSWORD=iklo postgres

$ docker service create --name drupal --network gpu_dmz -p 80:80 drupal

$ watch docker service ls ro

### Routing Mesh 

- ingress (incoming)
- IPVS from Linux Kernel 

$ docker service create --name search --replicas 3 -p 9200:9200 elasticsearch:2
$ docker service scale <serviceName>=4

$ docker service rollback <serviceName> --> rolls back to previous instances 