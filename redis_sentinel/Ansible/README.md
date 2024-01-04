# edit file vars.json

# run ansible playbook
```bash
ansible-playbook -i inventory.ini redis.yaml --extra-vars "@vars.json"
```

# check info redis 
```bash
redis-cli -h 172.16.10.20 -p 6379
AUTH basebs
INFO
```

# check info redis sentinel
```bash
redis-cli -h 172.16.10.20 -p 26379
INFO SENTINEL
```