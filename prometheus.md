### Test

ADMIN_USER=admin \
ADMIN_PASSWORD=parola \
docker stack deploy -c docker-compose.yml mon

### Staging

ADMIN_USER=swarm-staging \
ADMIN_PASSWORD=hyperion \
docker stack deploy -c docker-compose.yml mon

### Production

ADMIN_USER=swarm-prod \
ADMIN_PASSWORD=phobos \
docker stack deploy -c docker-compose.yml mon