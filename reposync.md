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

同步 epel 源到本地

cd /yum-server/epel7/

reposync --repoid=epel

createrepo  /yum-server/epel7/epel/

[https://github.com/openshift/openshift-ansible.git](https://github.com/openshift/openshift-ansible.git)

同步openshift 源到本地
```
cd /etc/yum.repos.d/

wget https://github.com/openshift/openshift-ansible/archive/release-3.6.zip  -O  openshift-ansible-release-3.6.zip

unzip  openshift-ansible-release-3.6.zip

cp /etc/yum.repos.d/openshift-ansible-release-3.6/roles/openshift_repos/templates/CentOS-OpenShift-Origin36.repo.j2   /etc/yum.repos.d/CentOS-OpenShift-Origin36.repo


cp /etc/yum.repos.d/openshift-ansible-release-3.6/roles/openshift_repos/files/origin/gpg_keys/openshift-ansible-CentOS-SIG-PaaS  /etc/pki/rpm-gpg/

cat /etc/yum.repos.d/CentOS-OpenShift-Origin36.repo 
[centos-openshift-origin36]
name=CentOS OpenShift Origin
baseurl=http://mirror.centos.org/centos/7/paas/x86_64/openshift-origin36/
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-SIG-PaaS

mkdir  /yum-server/openshift/

cd /yum-server/openshift/

reposync  --repoid=centos-openshift-origin36

createrepo  /yum-server/openshift/centos-openshift-origin36




```
设置  nginx  代理 仓库文件  在配置文件最后 添加一个虚拟主机

vim  /etc/nginx/nginx.conf

```
server {
    listen  80;
    server_name    172.16.100.249; # 自己PC的ip或者服务器的域名
    charset utf-8; # 避免中文乱码
    root /yum-server;
    location / {
        autoindex on; # 索引
        autoindex_exact_size on; # 显示文件大小
        autoindex_localtime on; # 显示文件时间
    }
}
```

设置 yum 仓库权限

```
chmod 755 -R  /yum-server
```

重启nginx 以更新配置文件
```
systemctl  restart nginx
```
