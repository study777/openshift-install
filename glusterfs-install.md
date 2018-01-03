配置 yum 源

### 基础源  CentOS-Base.repo

```
[base]
name=CentOS-$releasever - Base
baseurl=http://172.16.100.249/7-3-centos/base/ 
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

#released updates 
[updates]
name=CentOS-$releasever - Updates
baseurl=http://172.16.100.249/7-3-centos/updates/ 
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

#additional packages that may be useful
[extras]
name=CentOS-$releasever - Extras
baseurl=http://172.16.100.249/7-3-centos/extras/ 
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
```
### gluster 源  CentOS-Gluster-3.12.repo

```
[centos-gluster312]
name=CentOS-$releasever - Gluster 3.12
baseurl=http://172.16.100.249/centos-gluster312/centos-gluster312
gpgcheck=1
enabled=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-SIG-Storage
```



echo 'net.ipv6.conf.all.disable_ipv6 = 1'    >>  /etc/sysctl.conf 
sysctl  -p
systemctl stop NetworkManager
systemctl disable NetworkManager
systemctl  disable  firewalld
systemctl   stop   firewalld.service
sed -i 's/enforcing/disabled/g'  /etc/selinux/config
setenforce 0
sed -i 's/#AddressFamily any/AddressFamily inet/g'   /etc/ssh/sshd_config
sed -i 's/\#UseDNS yes/UseDNS no/g'   /etc/ssh/sshd\_config  
systemctl  restart sshd


yum install xfsprogs glusterfs-server  glusterfs glusterfs-fuse -y

