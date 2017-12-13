```
systemctl  stop docker

rm -rf /var/lib/docker/*
```

```
vim /etc/sysconfig/docker-storage-setup

DEVS=/dev/vdb
VG=docker-vg
SETUP_LVM_THIN_POOL=yes
```

```
lvmconf --disable-cluster

docker-storage-setup

systemctl  start docker

docker info


```