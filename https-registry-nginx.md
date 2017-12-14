

yum -y install docker-distribution

systemctl  start docker-distribution
systemctl  enable  docker-distribution


curl  172.16.100.247:5000/v2
<a href="/v2/">Moved Permanently</a>.


yum -y instal nginx
touch  /etc/nginx/conf.d/registry.conf


### create certs 

```
mkdir  /certs
cd /certs

openssl req -newkey rsa:4096 -nodes -sha256 -keyout   /certs/domain.key

Country Name (2 letter code) [XX]:  Enter
State or Province Name (full name) []:Enter
Locality Name (eg, city) [Default City]: Enter
Organization Name (eg, company) [Default Company Ltd]: Enter
Organizational Unit Name (eg, section) []:  Enter


Common Name (eg, your name or your server's hostname) []:devocr.paas.com

Email Address []: Enter
A challenge password []:Enter
An optional company name []:Enter




openssl req -newkey rsa:4096 -nodes -sha256 -keyout  /certs/domain.key   -x509  -days 356  -out  /certs/domain.crt

Common Name (eg, your name or your server's hostname) []:devocr.paas.com
```





systemctl  start nginx
systemctl  enable   nginx