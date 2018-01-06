---
tags: [python, devOps]
categories: software 	
---
# pre install
>## install pip
```sh
apt-get install python-pip python3-pip
```
>## change hostname
```sh
vi /etc/hostname
```
>## add master,minion ip2name mapping in this doc
```sh
vi /etc/hosts
```
# install salt-master
>## method1 
```sh
apt-get install salt-master
```
>## method2 http://repo.saltstack.com/
```sh
curl -L https://bootstrap.saltstack.com -o install_salt.sh
sudo sh install_salt.sh -P -M
```
# install salt-minion
>## method1 
```sh
apt-get install salt-minion
```
>## method2 http://repo.saltstack.com/
```sh
curl -L https://bootstrap.saltstack.com -o install_salt.sh
sudo sh install_salt.sh -P
```
# post install 
##	config minion
add master: $(master-host)

```sh
vi /etc/salt/minion
```
## accept key on master
```sh
salt-key - A
```
## test on master
```sh
salt '*' test.ping
```
# install salt-api on master
```sh
apt-get install salt-api
```
## create ssl crt key
```sh
salt-call --local tls.create_self_signed_cert
```
## create user using salt-api
```sh
adduser saltapi
passwd saltapi
```
## add config file 
```sh
vi /etc/salt/master.d/salt-api.conf
```
```
external_auth:
	pam:
		saltapi:
			- .*
rest_cherrypy:
	port: 8080
	host: 0.0.0.0
	#disable_ssl: True #http
	ssl_crt: /etc/pki/tls/certs/localhost.crt
	ssl_key: /etc/pki/tls/certs/localhost.key	
```

## start the salt-api service in debug mode
```sh
salt-api 2>&1 &
```
# errors

## TLSV1_ALERT_UNKNOWN_CA
change verify to False
## wrong version number
CherryPy is not compitable with ubuntu16.04,so change rest_tornado
## 401 Unauthorized
put token into header during the session

# directory structure

## cli
>command line management
## client
>an unified client interface include command line and net etc.
## grains
>functions return a dict, which will be assembled into grains dict

# debug mode
## salt-minion -l debug
## salt-master -l debug