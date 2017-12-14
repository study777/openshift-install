```
echo 'net.ipv6.conf.all.disable_ipv6 = 1'    >>  /etc/sysctl.conf 
sysctl  -p

sed -i 's/enforcing/disabled/g'  /etc/selinux/config
setenforce 0

systemctl stop NetworkManager
systemctl disable NetworkManager
systemctl  disable  firewalld
systemctl   stop   firewalld.service

sed -i 's/enforcing/disabled/g'  /etc/selinux/config
setenforce 0

sed -i 's/#AddressFamily any/AddressFamily inet/g'   /etc/ssh/sshd_config

```


```
yum -y install bind*

> /etc/named.conf
```

```
vim  /etc/named.conf

options {
directory "/var/named";
allow-query { 0.0.0.0/0; };
listen-on port 53 { any; };
};

zone "100.16.172.in-addr.arpa" {
type master;
file "172.16.100.zone";
};

zone "paas.com" {
type master;
file "paas.com.zone";
};
```


```
vim /var/named/172.16.100.zone

$TTL 3600
@             IN        SOA   100.16.172.in-addr.arpa. admin.example.com. (
                                 20190520
                                   1H
                                   15M
                                   1W
                                   1D)
             IN        NS        dns.paas.com.
249          IN        PTR       dns.paas.com.
223          IN       PTR        master01.paas.com.
224          IN       PTR        node01.paas.com.
225          IN      PTR         node02.paas.com.
226          IN      PTR         glusterfs01.paas.com.
227          IN      PTR         glusterfs02.paas.com.
228          IN      PTR         glusterfs03.paas.com.
229          IN      PTR         devocr.paas.com.
238          IN       PTR            .
```

```
vim /var/named/paas.com.zone

$TTL 3600
@                  IN  SOA  dns.paas.com. admin.paas.com. (
                        20190520
                        1H
                        15M
                       1W
                       1D)

                   IN  NS    dns.paas.com.
dns                IN   A    172.16.100.249
master01           IN   A    172.16.100.223
node01             IN   A    172.16.100.224
node02             IN   A    172.16.100.225
glusterfs01        IN   A    172.16.100.226
glusterfs02        IN   A    172.16.100.227
glusterfs03        IN   A    172.16.100.228
devocr             IN   A    172.16.100.229
*                 IN    A    172.16.100.238


```






```
systemctl start named

systemctl enable  named
```