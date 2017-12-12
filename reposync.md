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

chmod 755 -R  /yum-server





