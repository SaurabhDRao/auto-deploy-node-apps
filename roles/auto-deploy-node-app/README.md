Auto Deploy Node Apps
=========

This role clones a node app from github and deploys it into the specified VM.

Requirements
------------

1. The github account should have the public key of the control machine.
2. The private key file of the control machine should be stored in `files/id_rsa.github`

Role Variables
--------------

1. repo_url: The SSH URL of the repository where the app is.
```repo_url: git@github.com:gituser/Simple-Node-App.git```

Dependencies
------------

No dependencies as of yet

Improvements in Progress
------------

* Currently, the private key file of the github SSH key pair must be stored in `files/id_rsa.github`. This might become inconvenient, so will be providing a variable to specify the user defined path.

Example Playbook
----------------

    - hosts: servers
      become: yes
      roles:
      - role: auto-deply-node-app
        vars:
          repo_url: git@github.com:gituser/Simple-Node-App.git
