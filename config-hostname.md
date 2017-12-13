```
hostnamectl set-hostname  master07.paas.com

hostname -f
master07.paas.com


hostnamectl set-hostname  node08.paas.com
hostname -f
node08.paas.com


hostnamectl set-hostname  node09.paas.com
hostname -f
node09.paas.com


```



ssh-keygen -f ~/.ssh/id_rsa -N ''

for host in master07.paas.com node08.paas.com node09.paas.com ; do ssh-copy-id -i ~/.ssh/id_rsa.pub $host; done

