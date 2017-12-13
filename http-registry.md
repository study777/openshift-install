``
yum -y install docker-distribution

hostnamectl set-hostname  registry.paas.com

systemctl  start  docker-distribution

systemctl  enable   docker-distribution


``