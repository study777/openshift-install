准备工作

```
yum -y install nginx  yum-utils

systemctl start nginx

systemctl enable nginx

mkdir -p /yum-server/7-3-centos

mkdir -p /yum-server/epel7

```



同步 centos 源到至当前目录
```
cd  /yum-server/7-3-centos/

reposync --repoid=base

reposync --repoid=extras

reposync --repoid=updates

createrepo  /yum-server/7-3-centos/base/

createrepo  /yum-server/7-3-centos/extras/

createrepo  /yum-server/7-3-centos/updates/
```


同步 epel 源到本地
```


cd /yum-server/epel7/

reposync --repoid=epel

createrepo  /yum-server/epel7/epel/
```

同步openshift 源到本地
```
yum -y install centos-release-openshift-origin36.noarch

mkdir  /yum-server/openshift/

cd /yum-server/openshift/

reposync  --repoid=centos-openshift-origin36

createrepo  /yum-server/openshift/centos-openshift-origin36

删除 3.6.1  的包

cd /yum-server/openshift/

cp -r  centos-openshift-origin36   centos-openshift-origin360

cd centos-openshift-origin360/

rm -rf   *-3.6.1-*

createrepo  .


```

同步glusterFS 源到本地

```
yum -y install centos-release-gluster312.noarch

mkdir  /yum-server/centos-gluster312

cd /yum-server/centos-gluster312/

reposync  --repo=centos-gluster312

createrepo  /yum-server/centos-gluster312/centos-gluster312/

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
