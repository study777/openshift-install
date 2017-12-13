```
cd /root

wget https://github.com/openshift/openshift-ansible/archive/release-3.6.zip  -O  openshift-ansible-release-3.6.zip

yum -y install unzip

unzip  openshift-ansible-release-3.6.zip

> /root/openshift-ansible-release-3.6/roles/openshift_repos/templates/CentOS-OpenShift-Origin36.repo.j2

```



### /etc/ansible/hosts
```
[OSEv3:children]
masters
nodes
etcd
[OSEv3:vars]
openshift_clock_enabled=false
ansible_ssh_user=root
openshift_deployment_type=origin
openshift_release=3.6.0
openshift_master_default_subdomain=paas.com
openshift_master_identity_providers=[{'name': 'htpasswd_auth', 'login': 'true', 'challenge': 'true', 'kind': 'HTPasswdPasswordIdentityProvider', 'filename': '/etc/origin/master/htpasswd'}]
openshift_disable_check=memory_availability,disk_availability,docker_storage
oreg_url=devocr.paas.com/openshift/origin-${component}:${version}
openshift_examples_modify_imagestreams=true
openshift_docker_additional_registries=devocr.paas.com ,172.30.0.1/16:5000 
openshift_docker_insecure_registries=devocr.paas.com ,172.30.0.1/16:5000 
[masters]
master01.paas.com
[etcd]
master01.paas.com
node01.paas.com
node02.paas.com
[nodes]
node01.paas.com openshift_node_labels="{'region': 'infra', 'zone': 'default'}"
node02.paas.com openshift_node_labels="{'region': 'primary', 'zone': 'east'}"

```