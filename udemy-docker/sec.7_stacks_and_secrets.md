### Stacks 

$ docker stack deploy 

- deploy: --> in Compose file 
- build: --> can't do 
- swarm ignores build:; local compose ignores deploy:


$ docker stack deploy -c example-voting-app-stack.yml <stackname>
$ docker stack services <voteapp>
$ docker stack ps <voteapp>

### Secrets 

- /run/secrets/<secret-name> --> mounted only at this location 
- secure solution for storing secrets in Swarm 

$ docker secret create <name> <file>

$ echo "mypassword" | docker secret create psql_pass - --> creates a secret first; "-" is required 


$ docker service create --name psql --secret psql_user --secret psql_pass -e POSTGRES_PASSWORD_FILE=/run/secrets/psql_pass -e POSTGRES_PASSWORD_FILE=/run/secrets/psql_user postgres

$ docker exec -it <container name> bash

$ docker service update --secret-rm

$ docker secret ls 