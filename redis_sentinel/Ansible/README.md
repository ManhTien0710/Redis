# run ansible playbook
```bash
ansible-playbook -i inventory.ini redis.yaml --extra-vars "@vars.json"
```