#### eth0
```
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

#### eth1

```
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

#### bond0

```
DEVICE=bond0
TYPE=Ethernet
ONBOOT=yes
NM_CONTROLLED=no
GATEWAY=172.16.100.250
NETMASK=255.255.255.0
IPADDR=172.16.100.241
```

#### config dns

```
echo 'nameserver 172.16.100.247'    >   /etc/resolv.conf
```

