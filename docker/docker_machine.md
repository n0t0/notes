https://docs.docker.com/machine/drivers/

https://docs.docker.com/machine/reference/provision/

### Docker-machine install

$ base=https://github.com/docker/machine/releases/download/v0.16.0 &&
  curl -L $base/docker-machine-$(uname -s)-$(uname -m) >/tmp/docker-machine &&
  sudo install /tmp/docker-machine /usr/local/bin/docker-machine

$ docker-machine version

### Create a Host 

$ docker-machine --debug create --driver generic \
    --engine-storage-driver=devicemapper \
    <!-- --insecure-registry docker.ambrygen.com \ -->
    --generic-ip-address=<hostname_IP>  \
    --generic-ssh-user <user> \
    --generic-ssh-key ~/.ssh/id_rsa  \
    <hostname>

### Update Sudoers 

$ sudo visudo

<user> ALL=(ALL) NOPASSWD: ALL

### Make sure ssh-key is on a machine to be created

~/.ssh/id_rsa

### Storage driver to be used

- devicemapper

### Environment

docker-machine env <node>
eval $(docker-machine env <node>)
eval $(docker-machine env -u) --> undo

### Swarm 

### 01

- follow steps to create a host/s

$ docker-machine ssh <hostname> --> manager
$ docker swarm init --advertise-addr <hostname_IP> 

$ docker-machine ssh <hostname> --> worker
$ docker swarm join --token <token> <manager_hostname_IP:2377>

### 02

$ docker-machine create -d generic \
    --swarm \
    --swarm-master \
    --swarm-addr <hostnameIP> 
    --swarm-discovery token://<token> \
    --swarm-strategy binpack \
    --swarm-opt heartbeat=5s \
    upbeat
