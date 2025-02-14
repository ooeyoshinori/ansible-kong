## Procedure for GCP Ubuntu22.04 case
```bash
$ sudo apt update
$ sudo apt install -y ansible

$ ssh-keygen
$ cat $HOME/.ssh/id_rsa.pub
$ vim ~/.ssh/authorized_keys
# try to login targeted server by ssh

$ mkdir ansible-kong && cd ansible-kong
$ vim inventory.ini
[kong_servers]
${TARGETED_SERVER_ID_ADDRESS} ansible_user=${YOUR_ACCOUNT} ansible_ssh_private_key_file=~/.ssh/id_rsa ansible_python_interpreter=/usr/bin/python3

$ ansible -i inventory.ini kong_servers -m ping
${TARGETED_SERVER_ID_ADDRESS} | SUCCESS => {
    "changed": false,
    "ping": "pong"
}

$ mkdir -p ~/ansible-kong/roles/docker/tasks
$ mkdir -p ~/ansible-kong/roles/kong/tasks

$ vim ~/ansible-kong/roles/docker/tasks/main.yml
$ vim ~/ansible-kong/roles/kong/tasks/main.yml
$ vim ~/ansible-kong/playbook.yml

$ mkdir -p ~/ansible-kong/files
$ vim ~/ansible-kong/files/kong.yml
$ vim ~/ansible-kong/files/kong.conf

$ ansible-playbook -i inventory.ini playbook.yml

# Confirm to access URL below.
http://${TARGETED_SERVER_ID_ADDRESS}:8002
http://${TARGETED_SERVER_ID_ADDRESS}:8000/countries/1


# ####
# Directory
# ####
ansible-kong/
├── inventory.ini
├── playbook.yml
└── roles/
    ├── docker/
    │   ├── tasks/
    │   │   └── main.yml
    └── kong/
        ├── tasks/
        │   └── main.yml

# ####
# Tips
# ####
# network param on GCP
- kong-firewall
```