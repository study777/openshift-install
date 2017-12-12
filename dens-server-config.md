```
yum -y install bind*

> /etc/named.conf

vim  /etc/named.conf

options {
        directory "/var/named";
        allow-query     { 0.0.0.0/0; };
        listen-on port 53 { any; };
        };

zone "100.16.172.in-addr.arpa" {
        type master;
        file "172.16.100.zone";
};

zone "pass.com" {
        type master;
        file "pass.com";
};



vim /var/named/172.16.100.zone
```