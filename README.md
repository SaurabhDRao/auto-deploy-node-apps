# Auto Deploy Node Apps

This repository shows an example of how to use the auto-deploy-node-apps role.

### Prerequisites

* A set of remote machines that can be reached through passwordless ssh from the control machine.
* IP addresses of all those remote machines.
* A user with sudo privilages on those remote machines.

### How to Execute

1. Open the passwords.yml and add in the sudo passwords of all the remote hosts you want the app to be deployed on.
```
host_a_password: helloworld123
host_b_password: helloworld456
```

2. Open the inventory file in the directory and add in the IP addresses of the remote machines along with the username which has the sudo privilages and the sudo password variables.
```
192.168.0.3 ansible_user=myuser ansible_become_pass="{{ host_a_password }}"
host_b.xyz.com ansible_user=ansi ansible_become_pass="{{ host_b_password }}"
```

3. Open the root level main.yml and add in the SSH URL of the github repository in front of the `repo_url`.
```
repo_url: git@github.com:githubuser/Simple-Node-App.git
```

4. Run the below command in the project root directory
```
ansible-playbook -i inventory main.yml
```

### Known Issues

1. Sometimes an error occurs when updating the apt cache. Just comment out the below line in the appropriate task files.
```
update_cache: true
```

2. If you get error saying `/usr/bin/python3 does not exist`, then remove the below lines from the inventory file.
```
[all:vars]
ansible_python_interpreter=/usr/bin/python3
```

3. Currently, the private key file of the github SSH key pair must be stored in `roles/auto-deploy-node-app/files/id_rsa.github`. This might become inconvenient, so will be fixing it later.

4. Currently the passwords are stored as plain text. Will be using Ansible Vault later.