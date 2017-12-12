```
yum install -y ntp

ntpdate 1.asia.pool.ntp.org

> /etc/ntp.conf

vim  /etc/ntp.conf

driftfile /var/lib/ntp/drift
server 1.asia.pool.ntp.org
restrict default  nomodify
server  127.127.1.0     # local clock
fudge   127.127.1.0 stratum 10
includefile /etc/ntp/crypto/pw
keys /etc/ntp/keys

systemctl enable ntpd  
systemctl start ntpd  

```