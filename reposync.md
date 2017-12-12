yum -y install nginx  yum-utils

systemctl start nginx

systemctl enable nginx

mkdir -p /yum-server/7-3-centos

mkdir -p /yum-server/epel7


同步 centos 源到至当前目录

cd  /yum-server/7-3-centos/

reposync --repoid=base

reposync --repoid=extras

reposync --repoid=updates

createrepo  /yum-server/7-3-centos/base/

createrepo  /yum-server/7-3-centos/extras/

createrepo  /yum-server/7-3-centos/updates/





