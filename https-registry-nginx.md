

yum -y install docker-distribution

systemctl  start docker-distribution
systemctl  enable  docker-distribution


curl  172.16.100.247:5000/v2
<a href="/v2/">Moved Permanently</a>.


yum -y instal nginx
touch  /etc/nginx/conf.d/registry.conf





systemctl  start nginx
systemctl  enable   nginx