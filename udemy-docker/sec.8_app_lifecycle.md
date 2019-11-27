### Docker Override 

- docker-compose.override.yml 
- docker-compose.test.yml
- docker-compose.staging.yml
- docker-compose.prod.yml

$ docker-compose -f docker-compose.yml -f docker-compose.test.yml up -d 

$ docker-compose -f docker-compose.yml -f docker-compose.prod.yml config > output.yml --> that file will be used in production 

- extends: options doesn't work in Stacks 

### Service Updates 

$ docker service scale web=4 
$ docker service rollback <web> 
$ docker service update --image myapp:1.2.1 <service name> --> update a name 

$ docker service update --env-add NODE_ENV=prod --publish-rm 8080 --> combine 2 commands 

$ docker service scale web=8 api=6 --> scale multiple services 

$ docker stack deploy -c file.yml <stackname> --> deploy a stack

$ docker service update --force <service name>

