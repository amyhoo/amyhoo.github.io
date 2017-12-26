# install on ubuntu
>     apt-get update
>     apt-get install postgresql

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
>     psql -U username [-d database] [-h hostname]
>     psql exampledb < exampledb.sql 
>     createdb dbname
>     dropdb dbname
>     createuser username

#psql environment usage
>##schema
>>### show schema
>>     \dn
>>### create schema
>>     create schema 'xxx';
>>### drop schema
>>		drop schema 'xxx' [CASCADE];
>>### show search path
>>		show search_path;
>>### add schema into search path
>>		set search_path to 'schema_name',;

>##tablespace
>>### create tablespace
>>		create tablespace 'xxx' owner 'username' location 'path';

>##user
>>###list all user
>>		\du
>>### create role
>>		CREATE ROLE rolename [with password];
>>### create user
>>		CREATE USER username [with password];
>>### alter user password
>>		ALTER USER postgres WITH PASSWORD 'postgres';
>>### permission
>>		grant permission_type on tablename to rolename 
>>### show permission
>>		\z
>>###revoke permission
>>		REVOKE permission_type ON table_name FROM user_name;
>>###drop user group(role)
>>		drop role role_name;
 
>##database
>>###create databse
>>		CREATE DATABASE dbname;
>>###drop database
>>		drop database dbname;
>>###shift database
>>		\c dbname username serverIP port
>>###list all databases
>>		\l
>>###list all tables under database
>>		\d
>>###list connection information
>>		conninfo
>>### check schma
>>		\dn
>>### read sql from file
>>		\i

>##help, quit
>		\h
>		\?
>		\q

>##table
>>### show table's columns
>>		\d tablename
>>### show table information
>>		\d+ tablename