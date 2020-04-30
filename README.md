# Auto Deploy Node Apps

This repository shows how to automatically deploy node apps into a new VM. The main deployment role is present in `roles/auto-deploy-node-app` directory. The step by step configurations needed to execute the role is given below.

### Prerequisites

* A set of remote machines that can be reached through passwordless ssh from the control machine.
* IP addresses of all those remote machines.
* A user with sudo privilages on those remote machines.
> Make sure to check the prerequisites of the role in `roles/auto-deploy-node-app/README.md`

### How to Execute

The following steps are to be carried on the control machine.

1. Open the passwords.yml and add in the sudo passwords of all the remote hosts you want the app to be deployed on.
```
host_a_password: helloworld123
host_b_password: helloworld456
```

2. Use the below command to encrypt the `passwords.yml` file and enter the new vault password.
```ansible-vault encrypt passwords.yml```
    * If you want to make changes to the encrypted file, then use `ansible-vault decrypt passwords.yml` and enter the vault password.

3. Open the .vault-pass file and store in the vault password

3. Open the inventory file in the directory and add in the IP addresses of the remote machines along with the username which has the sudo privilages and the sudo password variables.
```
192.168.0.3 ansible_user=myuser ansible_become_pass="{{ host_a_password }}"
host_b.xyz.com ansible_user=ansi ansible_become_pass="{{ host_b_password }}"
```

4. Open the root level main.yml and add in the SSH URL of the github repository in front of the `repo_url`.
```
repo_url: git@github.com:githubuser/Simple-Node-App.git
```

5. Run the below command in the project root directory
```
ansible-playbook -i inventory main.yml --vault-password-file .vault-pass
```

### Improvements in Progress
* Will be adding roles to install databases. Currently it is assumed that the databases are present and running.

### Note
Check the readme in `roles/auto-deploy-node-app` folder for information on the role.