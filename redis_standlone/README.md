# download & install redis
```bash
yum install -y http://rpms.remirepo.net/enterprise/remi-release-7.rpm
yum --enablerepo=remi install -y redis
```
# config redis
```bash
vi /etc/redis.conf

change field
bind: 172.16.10.1
protection-mode no
requirepass passredis@
```
# check status redis
```bash
systemctl restart redis
systemctl status redis
systemctl enable redis
```
# login check redis server
```bash
redis-cli -c -h 172.16.10.1  -p 6379 -a 'passredis@'
```