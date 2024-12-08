# Simulate Ansible with Docker on a desktop setup

1. directories strucrure structure 

ansible-docker/
├── docker-compose.yml
├── control/
│   ├── Dockerfile
│   ├── ansible.cfg
│   ├── inventory
│   └── playbook.yml
├─── logs
├─── readme.md

2. docker-compose.yml
3. control/Dockerfile
4. control/ansible.cfg
5. control/inventory
6. control/playbook.yml

# Run the setup
docker-compose up --build

# Validate SSH connectivity
docker exec -it ansible_control bash
sshpass -p password ssh root@192.168.1.11
sshpass -p password ssh root@192.168.1.12

# Run Ansible Commands
ansible all -m ping
ansible-playbook playbook.yml

# Debug (if needed)

World Writable Directory Warning: Ensure /control has 755 permissions:

chmod 755 /control

Host Key Errors: Add the hosts' keys manually:

ssh-keyscan -H 192.168.1.11 >> ~/.ssh/known_hosts
ssh-keyscan -H 192.168.1.12 >> ~/.ssh/known_hosts

Inventory Not Found: Specify the inventory file explicitly:

ansible -i /control/inventory all -m ping
ansible-playbook -i /control/inventory playbook.yml