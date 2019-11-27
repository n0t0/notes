### docker-compose cli 

$ docker-compose up 
$ docker-compose down 

$ docker-compose logs 

### Compose to Build 

$ docker-compose build 

### More docker-composer cli 

$ docker-compose -d
$ docker-compose exec <psql> cat /run/secrets/psql_user

### Scale With docker-compose

$ docker-compose up -p <projectName> -d --scale web=3

### Pull Image

$ docker-compose pull --> do before docker-compose up

### Pause a Service/Stop 

$ docker-compose pause <service>
$ docker-compose unpause <service>
$ docker-compose stop 

### Monitor

$ docker-compose logs - 
$ docker-compose top
