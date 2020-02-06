#### Ref

https://elk-docker.readthedocs.io/
https://www.elastic.co/blog/beats-1-1-0-and-winlogbeat-released --> log stack

### Install

$ docker pull sebp/elk

### Increase Virtual Memory 

$ sudo sysctl -w vm.max_map_count=262144
$ echo 'vm.max_map_count=262144' >> /etc/sysctl.conf (to persist reboots)

### Run Container 

$ docker network create -d bridge elknet

$ docker run -p 5601:5601 -p 9200:9200 -p 9300:9300 -p 5044:5044 -d --network=elknet --name elk ambry/elk-cert

$ docker run -p 80:80 -d --name filebeat --network=elknet filebeat

$ docker run --mount -type=bind,source=/var/log/aex,target=/var/log/aex -p 8008:80 -d --name filebeat --network=elknetwork ambry-filebeat

docker run -p 80:80 -d --mount source=/var/log/,target=/var/log/ \--name filebeat --network=elknet filebeat

### docker-compose

- usav1svdckt1:/srv/elk

$ docker-compose up elk