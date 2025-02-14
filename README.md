## Procedure for GCP Ubuntu22.04(amd64) case
```bash
$ sudo apt update
$ sudo apt install -y ansible

$ ssh-keygen
$ cat $HOME/.ssh/id_rsa.pub

# Add public key on the targeted server
$ vim ~/.ssh/authorized_keys
# try to login targeted server by ssh and logout

$ cd ansible-kong
$ vim inventory.ini
[kong_servers]
${TARGETED_SERVER_IP_ADDRESS} ansible_user=${YOUR_ACCOUNT} ansible_ssh_private_key_file=~/.ssh/id_rsa ansible_python_interpreter=/usr/bin/python3

$ ansible -i inventory.ini kong_servers -m ping
${TARGETED_SERVER_IP_ADDRESS} | SUCCESS => {
    "changed": false,
    "ping": "pong"
}

$ ansible-playbook -i inventory.ini playbook.yml

# Confirm to access URL below via browser
http://${TARGETED_SERVER_IP_ADDRESS}:8002
http://${TARGETED_SERVER_IP_ADDRESS}:8000/countries/1


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