### Task Placement | Controlling Container Placement 

- service constraints (<key>=<value>)
- service modes (replicated|global)
- placement preferences (spread)
- node availability (active|pause|drain)
- resource requirements (cpu|memory)

### Service Constraints (hard requirement)

- node.labels --> execute from manager
- engine.labels --> change config, restart docker

#### place only on a manager

$ docker service create --constraint=node.role==manager nginx
$ docker service create --constraint=node.role!=worker nginx

#### add label to node2 for dmz=true

$ docker node update --label-add=dmz=true <node2>
$ docker service create --constraint=node.labels.dmz==true nginx

$ docker service update --constraint-rm node.role==worker --constraint-rm node.role==manager app1

$ docker node update --label-add dmz=true <node>
$ docker node update --label-rm dmz <node>
$ docker service create --name dmz-nginx --constraint node.labels.dmz==true --replicas 2 nginx 

### Service Modes 

- global --> one container on every node (add only with service creation)

$ docker service create --mode=global --name webserv nginx
$ docker service create --mode=global --name webserv --constraint=node.role==worker nginx

### Service Placement Preference 

- soft requirement 
- 'spread' 
- assign labels to nodes first 

$ docker node update --label-add azone=1 <nodeX>
$ docker node update --label-add azone=2 <nodeY>
$ docker node update --label-add azone=3 <nodeX>

$ docker service create --placement-pref spread=node.labels.azone --replicas 3 --name webapp1 nginx 

--placement-pref-add spread=node.labels.subnet
--placement-pref-rm spread=node.labels.subnet

$ docker service update --placement-pref-rm spread=node.labels.azone webapp1

### Node Availability 

- affects existing and new containers only 
- pause --> runs existing tasks, not available for new tasks (troubleshooting)
$ docker node update --availability=pause node2

- active --> runs existing tasks, available for new tasks
$ docker node update --availability=active node2

- drain --> reschedules existing tasks, not available for new tasks (maintenance)
$ docker node update --availability=drain node3 

### Resource Requirements 

- Limit CPU/Memory 
- OOME (Out Of Memory)**

$ docker service create --limit-memory 150M --limit-cpu .25 nginx 

- reservations are promises to services 
$ docker service create --reserve-memory 800M --reserve-cpu 1 mysql 

- update 
$ docker service update --limit-memory 0 --limit-cpu 0 myservice 


# Controlling Container Placement in Swarm

## Service Constraints

docker node ls

docker service create --name app1 --constraint node.role==worker nginx

docker service update --constraint-rm node.role==worker --constraint-add node.role=manager app1

docker node update --label-add dmz=true node2

docker service create --name dmz-nginx --constraint node.labels.dmz==true --replicas 2 nginx

## Service Mode

docker service create --mode=global --name test1 nginx

docker service ls

docker service rm test1

docker service create --mode=global --name test1 --constraint=node.role==worker nginx

## Service Placement Preference

http://docs.docker.com

docker node update --label-add azone=1 node1

docker node update --label-add azone=2 node2

docker node update --label-add azone=2 node3

docker service create --placement-pref=spread=node.labels.azone --replicas=2 --name webapp1 nginx

docker service create --placement-pref=spread=node.labels.azone --replicas=2 --name webapp2 nginx

docker service update --placement-pref-rm spread=node.labels.azone webapp1

docker service scale webapp2=8

docker service update --constraint-add node.role==worker webapp2

## Node Availability

docker service create --name webapp1 --replicas 4 nginx

docker node update --availability=pause node2

docker service update --replicas=8 webapp1

docker node update --availability=active node2

docker node update --availability=drain node3

docker node ls

docker node update --availability=active node3

## Service Resource Requirements

docker service create --reserve-memory 1000M --reserve-cpu 1 mysql

docker service create --reserve-memory 800M --name 800 nginx

docker service create --replicas 4 --reserve-memory 300M --name 300 nginx

docker service update --reserve-memory 0 800

docker service create --reserve-cpu 8 --name 8 nginx

docker service ps 8

docker service create --limit-memory 512M --name 100 bretfisher/stress:256m

docker service ps 100
