```
yum -y install ntpdate

echo '/usr/sbin/ntpdate 172.16.100.249  >> /var/log/ntpdate.log'   >> /etc/rc.local 



crontab -l
0 */2 * * * /usr/sbin/ntpdate  172.16.100.249


```