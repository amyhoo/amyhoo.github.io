---
categories: os
tags: [linux]    
---
# the usage of vps
## ssr
### install shadowsocksR service on your vps
```
wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocksR.sh

chmod +x shadowsocksR.sh

./shadowsocksR.sh 2>&1 | tee shadowsocksR.log
```

### install shadowsocks service on your vps
```
wget --no-check-certificate -O shadowsocks.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh
chmod +x shadowsocks.sh
./shadowsocks.sh 2>&1 | tee shadowsocks.log
```
### install the client on your pc
pay attention, you should use most strict protection, otherwise, still not work on some machine ; for example: use chacha as encryption

