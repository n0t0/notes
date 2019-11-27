### Healthcheck 

- docker engine will exec (e.g. curl localhost)

- exit 0 (OK)
- exit 1 (Error)

### Container States 

- starting 
- healthy 
- unhealthy 

### Healthcheck Status

$ docker container ls 
$ docker container inspect 


$ docker run \
    --health-cmd="curl -f localhost:9200/_cluster/health || false" \ 
    --health-interval=5s \
    --health-retries=3 \
    --health-timeout=2s \ 
    --health-start-period=15s \
    elasticsearch:2 

### Healhcheck Options 

- --interval=DURATION (default: 30s)
- --timeout=DURATION (default: 30s)
- --start-period=DURATION (default: 0s) 
- --retries=N (default: 3)


$ HEALTHCHECK curl -f http://localhost/ || false 

$ HEALTHCHECK --timeout=2s --interval=3s --retries=3 \ 
  CMD curl -f http://localhost/ || exit 1


### Healthcheck in Nginx Dockerfile 

FROM nginx:1.13

HEALTHCHECK --interval=30s --timeout=3s \ 
 CMD curl -f http://localhost/ || exit 1 

 
 $ docker container run --name psql -d --health-cmd="pg_isready -U postgres || exit 1" postgres 

 $ docker service create --name p2 --health-cmd="pg_isready -U postgres || exit 1" postgres 