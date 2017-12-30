---
categories: 	
    - "devOps"
---
# pre install
>## install pip
>		apt-get install python-pip python3-pip
>## change hostname
>		vi /etc/hostname
>## add master,minion ip2name mapping in this doc
>		vi /etc/hosts

# install salt-master
>## method1 
>		@master# apt-get install salt-master
>## method2 http://repo.saltstack.com/
>		@master# curl -L https://bootstrap.saltstack.com -o install_salt.sh
>		@master# sudo sh install_salt.sh -P -M

# install salt-minion
>## method1 
>		@minion# apt-get install salt-minion
>## method2 http://repo.saltstack.com/
>		@minion# curl -L https://bootstrap.saltstack.com -o install_salt.sh
>		@minion# sudo sh install_salt.sh -P

# post install 
##	config minion
add master: $(master-host)
>		@minion# vi /etc/salt/minion
## accept key on master
>		@master# salt-key - A

## test on master
>		@master# salt '*' test.ping

# install salt-api on master
>		@master# apt-get install salt-api
## create ssl crt key
>		@master# salt-call --local tls.create_self_signed_cert
## create user using salt-api
>		@master# adduser saltapi
>		@master# passwd saltapi
## add config file 
>		@master# vi /etc/salt/master.d/salt-api.conf
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
## start the salt-api service
>		salt-api 2>&1 &


# errors
## TLSV1_ALERT_UNKNOWN_CA
change verify to False
## wrong version number
CherryPy is not compitable with ubuntu16.04,so change rest_tornado
## 401 Unauthorized
put token into header during the session
