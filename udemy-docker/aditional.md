### Service Logs 

- return all logs for a service 
$ docker service logs <servicename/id>
- return all logs for a single task
$ docker service logs <taskid>
- unformatted logs
$ docker service logs --raw --no-trunc <servicename/id>
- tail/follow
$ docker service logs --tail 50 --follow <servicename/id>

--
$ docker exec $(docker ps --filter name=vote_vote -q) ./generate-some-votes.sh
$ docker service logs vote_worker 2>&1 | grep <transaction id>

### Docker Events 

$ docker events 
$ docker events --since 2017-12-01
$ docker events --since 30m
$ docker events --since 1h --filter event=start
$ docker events --since 1h --filter scope=swarm --filter type=network 

### First Swarm Service

$ docker service create --name webserver --replicas 3 --detach=false --publish 8080:80 nginx 

- docker swarm
- docker node
- docker service
- docker stack
- docker secret 

- manager is a worker with permissions to control the swarm 

$ docker service create --> used in swarm instead of _docker container run_

$ docker service ps <service>

$ docker update --help
$ docker service update --help

### docker-machine

$ docker-machine create <node1>

$ docker-machine ssh <node1> 
$ docker-machine env <node1> --> both connect to the machine 

$ docker exec $(docker ps --filter name=vote_vote -q) ./generate-some-votes.sh

$ docker service scale <service>=0

### Swarm Configs 

- create a new Config from a nginx config 
$ docker config create nginx01 ./nginx.conf 

- create a Service with a Config 
$ docker service create --config source-nginx01, target=/etc/nginx/conf.d/default.conf 

- create new config o replace old 
$ docker config create nginx02 ./nginx.conf 

- update Service with new Config 
$ docker service update --config-rm nginx01 --config-add source=nginx02, target=/etc/nginx/conf.d/default.conf 


$ docker service create --config source=vote-nginx-20171211,target=/etc/nginx/conf.d/default.conf -p 9000:80 --network vote_frontend --name proxy nginx 

$ docker config inspect vote-nginx-20171211 