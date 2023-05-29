# install haproxy
```bash
yum install -y haproxy
yum provides /usr/sbin/semanage
yum install -y policycoreutils-python
```
# config haproxy
```bash
vi /etc/haproxy/haproxy.cfg
vi /usr/lib/systemd/system/haproxy.service
```
# open port
```bash
sudo semanage port -a -t http_port_t  -p tcp 8404
firewall-cmd --add-port=8404/tcp --permanent
firewall-cmd --add-port=6379/tcp --permanent
firewall-cmd --reload
```
# config log
```bash
sed -i "s/#\$ModLoad imudp/\$ModLoad imudp/g" /etc/rsyslog.conf
sed -i "s/#\$UDPServerRun 514/\$UDPServerRun 514/g" /etc/rsyslog.conf
echo '$UDPServerAddress 127.0.0.1' >> /etc/rsyslog.conf
echo 'local2.*    /var/log/haproxy.log' > /etc/rsyslog.d/haproxy.conf
systemctl restart rsyslog
```

# check status haproxy
```bash
systemctl restart haproxy.service
systemctl status haproxy.service
systemctl enable haproxy.service
```
# check log
```bash
tail /var/log/haproxy.log -n 100 -f
```
# Check login redis through haproxy
```bash
redis-cli -c -h 172.16.10.1  -p 6379 -a 'redispass@'
```