## server  config

```
yum -y install docker-distribution  nginx


systemctl  start docker-distribution
systemctl  enable  docker-distribution


curl  172.16.100.247:5000/v2
<a href="/v2/">Moved Permanently</a>.
```




###  cat /etc/nginx/conf.d/registry.conf
```
upstream docker-registry {  
  server devocr.paas.com:5000;  
}  

server {  
  listen 443;  
  server_name devocr.paas.com;  

  # SSL  
  ssl on;  
  ssl_certificate /certs/domain.crt;  
  ssl_certificate_key /certs/domain.key;  

  # disable any limits to avoid HTTP 413 for large image uploads  
  client_max_body_size 0;  

  # required to avoid HTTP 411: see Issue #1486 (https://github.com/docker/docker/issues/1486)  
  chunked_transfer_encoding on;  

  location / {  
    # Do not allow connections from docker 1.5 and earlier  
    # docker pre-1.6.0 did not properly set the user agent on ping, catch "Go *" user agents  
    if ($http_user_agent ~ "^(docker\/1\.(3|4|5(?!\.[0-9]-dev))|Go ).*$" ) {  
      return 404;  
    }  

    # To add basic authentication to v2 use auth_basic setting plus add_header  
    # auth_basic "registry.localhost";  
    # auth_basic_user_file /etc/nginx/conf.d/registry.password;  
    # add_header 'Docker-Distribution-Api-Version' 'registry/2.0' always;  

    proxy_pass                          http://docker-registry;
    proxy_set_header  Host              $http_host;   # required for docker client's sake  
    proxy_set_header  X-Real-IP         $remote_addr; # pass on real client's IP  
    proxy_set_header  X-Forwarded-For   $proxy_add_x_forwarded_for;  
    proxy_set_header  X-Forwarded-Proto $scheme;  
    proxy_read_timeout                  900;  
  }  

}  

```





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

-days 356  -out  /certs/domain.crt
Country Name (2 letter code) [XX]:Enter
State or Province Name (full name) []: Enter
Locality Name (eg, city) [Default City]: Enter
Organization Name (eg, company) [Default Company Ltd]:Enter
Organizational Unit Name (eg, section) []:Enter

Common Name (eg, your name or your server's hostname) []:devocr.paas.com

Email Address []: Enter
```

###  test  on  server
```
systemctl  start nginx
systemctl  enable   nginx
cat /certs/domain.crt    >> /etc/pki/tls/certs/ca-bundle.crt
curl  https://devocr.paas.com/v2
<a href="/v2/">Moved Permanently</a>.

```




## client  config

mkdir  /etc/docker/certs.d/devocr.paas.com
scp devocr.paas.com:/certs/domain.crt   /etc/docker/certs.d/devocr.paas.com/
cat /etc/docker/certs.d/devocr.paas.com/domain.crt    >> /etc/pki/tls/certs/ca-bundle.crt
echo "ADD_REGISTRY='--add-registry devocr.paas.com'"   >> /etc/sysconfig/docker



systemctl  restart docker

### curl test on clinet
curl  https://devocr.paas.com/v2
<a href="/v2/">Moved Permanently</a>.


curl  devocr.paas.com:5000/v2
<a href="/v2/">Moved Permanently</a>.


###  docker  push  on  client



###  docker  pull  on  client

##### remove  all  local  images

```
docker rmi $(docker images -q)  -f

```


```
docker pull devocr.paas.com/heketi/heketi:latest

docker pull devocr.paas.com/openshift/hello-openshift:latest

docker pull devocr.paas.com/cockpit/kubernetes:latest


```













