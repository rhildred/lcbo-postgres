lcbo database

```bash
pip install --user ansible
ansible-playbook up.yml
```

This brings up an old lcbo database. 

```bash
ansible-playbook down.yml
```

This does docker compose down on the `docker-compose.yml` (the same docker-compose file from up.yml)
