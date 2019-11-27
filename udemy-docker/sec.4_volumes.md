### Container Lifetime 

- immutable containerse --> only re-deploy, never change 

### Persistend Data Volumes 

$ docker volume ls 

$ docker container run -d --name mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=True -v mysql-db:/var/lib/mysql mysql

$ docker create volume --> crate ahead of time to change driver 

### Persistend Data Bind Mounting 

$ docker container run -d --name nginx -p 80:80 -v $(pwd):/usr/share/nginx/html nginx 

