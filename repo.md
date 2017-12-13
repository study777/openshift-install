```
cat /etc/yum.repos.d/CentOS-Base.repo 
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

```
cat /etc/yum.repos.d/CentOS-OpenShift-Origin.repo 
[openshift]
name=openshift
baseurl=http://172.16.100.249/openshift/centos-openshift-origin36/ 
gpgcheck=0
enabled=1
```

```
cat /etc/yum.repos.d/epel.repo 

[epel]
name=epel
baseurl=http://172.16.100.249/epel7/epel/
gpgcheck=0
enabled=1

```

