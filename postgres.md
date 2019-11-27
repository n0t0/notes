#### Install PostgreSQL

sudo yum install postgresql-server postgresql-contrib --disablerepo=* --enablerepo=Ambry*


#### Initialize a Database

sudo postgresql-setup initdb

#### Update File (replace both lines 'ident' with 'md5')

sudo vi /var/lib/pgsql/data/pg_hba.conf 

host    all             all             127.0.0.1/32            ident
host    all             all             ::1/128                 ident

### su user

sudo -i -u postgres

### Create and Delete DB

createdb <database> --> shell
create database <database>; --> sql

dropdb <database> --> shell
drop database <database> --> sql

\l --> list databases

### Tables 

\d --> list tables 
\dt --> list just tables

### Users and Roles 

createuser --> shell command same as CREATE USER <user>; 
\du --> list users 
\password --> change password 

hidden_hippo
h!pP()


### Connect to a Server

psql -U <user> -d <database> -h <host> -W
\c connect to a database


### Misc

psql 
postgres=# SHOW config_file;


### Permissions

- revoke access to public and user; ALL not an option

revoke create on schema public from public;
revoke create on schema public from <user>;


### Schemas 

CREATE SCHEMA IF NOT EXISTS <schema> AUTHORIZATION <user>;

hidden_hippo
dalj#@LGJWdjakl

