# install redis
```bash
yum install -y http://rpms.remirepo.net/enterprise/remi-release-7.rpm
yum --enablerepo=remi install -y redis
```
# config redis_server on 3 server: change IP, port, pass for redis
```bash
vi /etc/redis.conf
vi /usr/lib/systemd/system/redis.service
```
# permision
```bash
chown -R redis:redis /var/log/redis
sudo chown -R redis:redis /var/lib/redis
```
# open port
```bash
firewall-cmd --add-port=6379/tcp --permanent
firewall-cmd --add-port=16379/tcp --permanent
firewall-cmd --add-port=8107/tcp --permanent
firewall-cmd --add-port=18107/tcp --permanent
firewall-cmd --reload
```
# config memory
```bash
echo "
vm.overcommit_memory = 1
" >> /etc/sysctl.conf
```
# check status redis
```bash
systemctl restart redis
systemctl status redis
systemctl enable redis
```
# config redis-replica on 3 server: change IP, port, pass for redis
```bash
vi /etc/redis-replica.conf
vi /usr/lib/systemd/system/redis-replica.service
```
# permision
```bash
sudo chown -R redis:redis /etc/redis-replica.conf
sudo chown -R redis:redis /var/lib/node-replica.conf
```
# check status redis-replica
```bash
systemctl restart redis-replica.service
systemctl enable redis-replica.service
systemctl status redis-replica.service
```
# **if need to restart, should restart replica before

# cluster nodes
```bash
redis-cli --cluster create 172.16.10.1:6379 172.16.10.2:6379 172.16.10.3:6379 172.16.10.1:8107 172.16.10.2:8107 172.16.10.3:8107 --cluster-replicas 1 -a 'passredis@'
```
# test cluster
```bash
redis-cli -c -h 172.16.10.1 -p 6379 -a 'passredis@'
INFO
cluster nodes
```
# if cluster fail: on 3 server
```bash 
cd /var/lib/redis/
rm -rf *

redis-cli --cluster create 172.16.10.1:6379 172.16.10.2:6379 172.16.10.3:6379 172.16.10.1:8107 172.16.10.2:8107 172.16.10.3:8107 --cluster-replicas 1 -a 'passredis@'
```