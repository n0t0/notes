### Registries 

- Docker Hub
- Docker Store (store.docker.com)
- Docker Cloud (cloud.docker.com)


- link accounts with hub.docker.com

### Docker Store 

- docker software 
- higher level of insurance from 3rd parties 

### Docker Cloud CI/CD and Server Ops

- docker swarm 

### Registry 

- --registry-mirror 
- certificates 

$ docker container run -d -p 5000:5000 --name registry registry 

$ docker tag hello-world 127.0.0.1:5000/hello-world --> create official image at the root of the registry 

$ docker push 127.0.0.1:5000/hello-world 
$ docker pull 127.0.0.1:5000/hello-world 


$ docker container kill registry 
$ docker container rm registry 

$ docker container run -d -p 5000:5000 --name registry -v(pwd)/registry-data:/var/lib/registry registry


$ docker -run -d -p 5000:5000 --name registry \
    --restart unless-stopped \
    -v $(pwd)/registry-data:/var/lib/registry -v $(pwd)/certs:/certs \
    -e REGISTRY_HTTP_TLS_CERTIFICATE=/certs/domain.crt \ 
    -e REGISTRY_HTTP_TLS_KEY=/certs/domain.key \
    registry 