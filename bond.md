```
vi /etc/sysconfig/network-scripts/ifcfg-eth0

DEVICE=eth0
TYPE=Ethernet
BOOTPROTO=none
NAME=eth0
ONBOOT=yes
MASTER=bond0
USERCTL=no
SLAVE=yes
NM_CONTROLLED=no

```

```
vi  /etc/sysconfig/network-scripts/ifcfg-eth1

DEVICE=eth1
TYPE=Ethernet
BOOTPROTO=none
NAME=eth1
ONBOOT=yes
MASTER=bond0
USERCTL=no
SLAVE=yes
NM_CONTROLLED=no
```


```
vi  /etc/sysconfig/network-scripts/ifcfg-bond0

DEVICE=bond0
TYPE=Ethernet
DNS1=172.16.100.249
ONBOOT=yes
NM_CONTROLLED=no
GATEWAY=172.16.100.250
NETMASK=255.255.255.0
IPADDR=172.16.100.230

```


```
vi /etc/modprobe.d/bonding.conf

alias bond0 bonding
options bond0 miimon=100 mode=1
```

```
modprobe bonding
lsmod | grep bonding

systemctl   restart network

reboot


```









