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
# install master and minion
sudo sh install_salt.sh -P -M
# install minion
sudo sh install_salt.sh -M
# install syndic
sudo sh install_salt.sh -S
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
add-apt-repository ppa:saltstack/salt
apt-get update
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
## salt-api
### TLSV1_ALERT_UNKNOWN_CA
change verify to False
### wrong version number
CherryPy is not compitable with ubuntu16.04,so change rest_tornado
### 401 Unauthorized
put token into header during the session

## salt authentication
# remove master key on minion
```sh
rm /etc/salt/pki/minion/minion_master.pub
```
# remove minion key from master
```sh
 rm /etc/salt/pki/minion/{minion_key}
```

# directory structure

## cli
>command line management
## client
>an unified client interface include command line and net etc.
## grains
>functions return a dict, which will be assembled into grains dict

# debug mode
```sh
salt-minion -l debug
salt-master -l debug
salt-syndic -l debug
```
# check logs
```sh
tail -f /var/log/salt/minion
tail -f /var/log/salt/syndic
```
# check version
```sh
salt-master --version
salt --versions-report
```

# important categories
## /etc/salt
## /var/log/salt/
## /var/cache/salt
## /etc/salt/pki/

# authentication
```
salt-run manage.down removekeys=True
```
# minion init
```
send a minion_pub_key to master
master store the minion_pub_key in /etc/salt/pki/master/minions
master send master_pub_key to minion
minion store the master_pub_key in /etc/salt/pki/minion/minion_master.pub
```

# workflow of salt
```
There's a spectrum of workflows, depending on how much detail you need and when.

True fire-and-forget - POST to the /hook interface.
Fire a job, get a JID, look up the result later - POST to / or /run with one of the *_async client interfaces. Or POST to /minions.
Fire a job and synchronously wait for the result - POST to / or /run with one of the synchronous client interfaces. You can lean on the timeout kwarg to adjust how long the connection should say open although for very long connections this like likely to run afoul of some HTTP timeout somewhere (server, client, somewhere in between, etc.)
Watch for job new and job return events by watching the event stream at /events. This endpoint is tailor-made for long-lived connections. You can run async jobs as normal and watch the result on the event bus.
```

# change setting dynamically
```sh
salt -t 60
```

# cluster update
## find information and record it
```sh
salt '*' test.versions_report
salt '*' pkg.list_upgrades
salt "*" pkg.lastest_version salt-minion
```
## first update salt-master 
```
```
## second update salt-syndic

## three update salt-minion
