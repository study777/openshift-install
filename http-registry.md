``
yum -y install docker-distribution

hostnamectl set-hostname  registry.paas.com

systemctl  start  docker-distribution

systemctl  enable   docker-distribution

yum -y install docker

echo "INSECURE_REGISTRY='--insecure-registry registry.paas.com:5000'"    >> /etc/sysconfig/docker

systemctl  restart docker



docker tag docker.io/heketi/heketi:latest  registry.paas.com:5000/heketi/heketi:latest
docker push registry.paas.com:5000/heketi/heketi:latest


docker tag docker.io/cockpit/kubernetes:latest  registry.paas.com:5000/cockpit/kubernetes:latest
docker push registry.paas.com:5000/cockpit/kubernetes:latest

docker tag docker.io/openshift/origin-deployer:v3.6.0  registry.paas.com:5000/openshift/origin-deployer:v3.6.0
docker push registry.paas.com:5000/openshift/origin-deployer:v3.6.0

docker tag docker.io/openshift/origin-haproxy-router:v3.6.0  registry.paas.com:5000/openshift/origin-haproxy-router:v3.6.0
docker push registry.paas.com:5000/openshift/origin-haproxy-router:v3.6.0




docker tag docker.io/openshift/origin-service-catalog:latest   registry.paas.com:5000/openshift/origin-service-catalog:latest

docker push registry.paas.com:5000/openshift/origin-service-catalog:latest



docker tag docker.io/openshift/hello-openshift:latest   registry.paas.com:5000/openshift/hello-openshift:latest
docker push registry.paas.com:5000/openshift/hello-openshift:latest
 

docker tag docker.io/centos/mysql-57-centos7:latest   registry.paas.com:5000/centos/mysql-57-centos7:latest 
docker push registry.paas.com:5000/centos/mysql-57-centos7:latest









``