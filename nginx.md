### log formating for nginx X
```
log_format combined_plus_rt '$remote_addr - $remote_user [$time_local]'
                                 '"$request" $status $body_bytes_sent '
                                 '"$http_referer""$http_user_agent" $request_time' ;
```

### Location Blocks - Matching Requests
```
location /greet {
	return 200 ‘return a string match’;
}

location = /greet {
	return 200 ‘return an exact string match’;
}

location = ~ /greet[0-9] {
	return 200 ‘return a case sensitive regex match’;
}


location = ~* /greet[0-9] {
	return 200 ‘return a case insensitive regex match’;
}

location = ^~ /greet[0-9] {
	return 200 ‘return a preferential match’;
}
```

### Logging
```
location /downloads {

	access_log off;
	error_log /var/log/nginx/downloads.error.log;

	root /sites;
	try_file $uri =404;
}
```

### Inheritance & Directives Types

Standart Directive

gzip on; —> global unless turned off in location downwards

Array Directive —> defined multiple times with diff values

Action Directive —> does action like return or rewrite

try_files $uri =404;—> look for $uri variable first or return error

### Configuring a Backend
```
sudo yum install php5-fpm
sudo yum install php5-mysql
sudo yum install php5
sudo yum install php5-cgi
```
- /etc/php5/fpm/www.conf —> make php and nginx listen to the same port

### Configuring Nginx Workers

$ ulimit -n —> use that number for worker_connections 1024;

- add_header X-Frame-Options SAMEORIGIN;

### Dynamic Modules

### Expires Headers

### Gzip
```
gzip on;
gzip_min_lenght 100;
gzip_comp_level 3; —> the higher the level the more compression is applied but more resources are used (keep between 2 and 4)

gzip_types text/plain;
gzip_types text/css;
gzip_types text/javascript;

gzip_disalbe “msie6”; —> Microsft Internet Explorer 6
```