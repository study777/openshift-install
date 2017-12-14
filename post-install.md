```
echo 'NM_CONTROLLED=no'  >>  /etc/sysconfig/network-scripts/ifcfg-eth0

echo 'NM_CONTROLLED=no'  >>  /etc/sysconfig/network-scripts/ifcfg-eth1

echo 'NM_CONTROLLED=no'  >>  /etc/sysconfig/network-scripts/ifcfg-bond0 

```


systemctl  stop NetworkManager

systemctl  restart network