# lcbo database

```bash
pip install --user ansible
ansible-playbook up.yml
```

This brings up an old lcbo database. The database is on a network signoz-net. This is so that it can be used with an otel collector on that network. You can compose this with an otel collector by including this repo as a submodule. There is an example of this at https://github.com/conestogac-acsit/cdevops-signoz. If you do this you will want to include the tasks.yml in your playbook so that the docker-compose.yml gets included with other submodules on the same network. You can see this in up.yml

```yaml
- name: bootstrap lcbo database
  hosts: localhost
  gather_facts: false  
  tasks:
    - name: docker compose up
      community.docker.docker_compose_v2:
        project_src: .
        files:
        - docker-compose.yml
        state: present
    - import_tasks: tasks.yml
      vars:
        db_user: lcbo
        db_name: lcbo
        db_password: Secret5555
        connect_user: 'devtedsuser'
        connect_password: 'devtedspass'
        connect_host: 'localhost'
```

## `down.yml`

```bash
ansible-playbook down.yml
```

This does docker compose down on the `docker-compose.yml` (the same docker-compose file from up.yml)

## The data

There is a short Jupyter notebook, `products.ipynb`, that you can use as an example to consume data from this database. Just click on it in vscode, install the python extension if it prompts you for it. You will see data from the products table. 