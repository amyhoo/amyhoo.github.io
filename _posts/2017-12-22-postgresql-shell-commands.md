---
categories: database    
---

# install on ubuntu
```sh
apt-get update
apt-get install postgresql
```

# change login mode 
>edit file pg_hba.conf
>1. peer mode
>>support local connection using system user name ,default
>2. md5 mode 
>>it is password-based authentication 
>3. change line "local all postgres peer" to "local all postgres md5"
>4. add a line below IPv4 "host all all	ip/32|24|16|0	md5"
>>allow ip addresses in IPv4

>edit file postgresql.conf
>1. change line "#listen_addresses='localhost'" to "listen_addresses='*'"
>>allow remote access

# cmd usage
```sh
psql -U username [-d database] [-h hostname]
psql exampledb < exampledb.sql 
createdb dbname
dropdb dbname
createuser username
```

# psql environment usage
>## schema
>>### show schema
```sh
# into psql
\dn
```

>>### create schema
```sh
# into psql
create schema 'xxx';
```

>>### drop schema
```sh
# into psql
drop schema 'xxx' [CASCADE];
```

>>### show search path
```sh
# into psql
show search_path
```

>>### add schema into search path
```sh
# into psql
set search_path to 'schema_name'
```	

## tablespace
>>### create tablespace
```sh
# into psql
create tablespace 'xxx' owner 'username' location 'path';
```

>## user
>>### list all user
```sh
# into psql
\du
```

>>### create role
```sh
# into psql
CREATE ROLE rolename [with password];
```

>>### create user
```sh
# into psql
CREATE USER username [with password];
```

>>### alter user password
```sh
# into psql
ALTER USER postgres WITH PASSWORD 'postgres'
```		

>>### permission
```sh
# into psql
grant permission_type on tablename to rolename 
```	

>>### show permission
```sh
# into psql
\z
```

>>### revoke permission
```sh
# into psql
REVOKE permission_type ON table_name FROM user_name;
```

>>### drop user group(role)
```sh
# into psql
drop role role_name;
```	

>## database
>>### create databse
```sh
# into psql
CREATE DATABASE dbname;
```	

>>### drop database
```sh
# into psql
drop database dbname;
```

>>### shift database
```sh
# into psql
\c dbname username serverIP port
```

>>### list all databases
```sh
# into psql
\l
```

>>### list all tables under database
```sh
# into psql
\d
```

>>### list connection information
```sh
# into psql
conninfo
```

>>### check schma
```sh
# into psql
\dn
```

>>### read sql from file
```sh
# into psql
\i
```

>## help, quit
```sh
# into psql
\h
\?
\q
```		

>## table
>>### show table's columns
```sh
# into psql
\d tablename
```

>>### show table information
```sh
# into psql
\d+ tablename
```