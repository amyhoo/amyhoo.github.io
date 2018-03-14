---
tags: [python, devOps]
categories: software 	
---
# make install
```sh
# download this software xxx.tar.gz and tar into directory xxx
# tar jxvf xxx.tar.bz2
tar xvzf xxx.tar.gz
cd xxx
# set up the custom installed path
./configure --prefix=/usr/local
make --jobs=`grep processor /proc/cpuinfo | wc -l`
make install
```

# install saltstack
## tools of make install
gcc
make
automake
python2.7.12
## tools of dev
```sh
apt-get install libtool autoconf automake
apt-get install uuid-dev g++
apt-get install python-dev
# libsodium18
apt-get install libsodium18
```
 
## basic
### python packages 
```sh
pip install cherrypy==3.2.3
pip install python-dateutil==2.4.2
pip install gitdb==0.6.4
pip install gitpython==1.0.1
pip install Jinja2==2.8
pip install Mako==1.0.3
pip install msgpack-python==0.4.6
pip install pycrypto==2.6.1
pip install PyYAML==3.11
pip install PyZMQ==15.2.0
#pip install smmap==0.9.0
pip install Tornado==4.2.1

# docker-py: Not Installed
# ioflo: Not Installed
# libgit2: Not Installed
# libnacl: Not Installed
# M2Crypto: Not Installed
# msgpack-pure: Not Installed
# mysql-python: Not Installed
# pycparser: Not Installed
# pycryptodome: Not Installed
# pygit2: Not Installed         
# python-gnupg: Not Installed
# RAET: Not Installed
# timelib: Not Installed
```
### support tools
```sh
# install ZMQ=4.1.4
wget http://download.zeromq.org/zeromq-4.1.4.tar.gz
tar -zxvf zeromq-4.1.4.tar.gz
./configure --prefix=/usr/local
make
make install
```

### environment
```sh
wget -O - https://repo.saltstack.com/apt/ubuntu/16.04/amd64/latest/SALTSTACK-GPG-KEY.pub | sudo apt-key add -
vi /etc/apt/sources.list.d/saltstack.list
#deb http://repo.saltstack.com/apt/ubuntu/16.04/amd64/latest xenial main
apt-get update

#pip install --install-option="--prefix=/app/salt" --ignore-installed salt
pip install --target=/app/salt salt

```
## saltstack master
```sh
apt-get download salt-master
```

## saltstack syndic
```sh
apt-get download salt-syndic
```
## saltstack minion
```sh
apt-get download salt-minion
```
## saltstack api
```sh
apt-get download salt-api
```

## setup links
```sh
```