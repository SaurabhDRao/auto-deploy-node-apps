Auto Deploy Node Apps
=========

This role clones a node app from the git hub and deploys it into the specified VM.

Requirements
------------

1. The github account should have the public key of the control machine.
2. The private key file stored in the role's files directory with the filename id_rsa.github

Role Variables
--------------

1. repo_url: The SSH URL of the repository where the app is.
Ex: ```repo_url: git@github.com:gituser/Simple-Node-App.git```

Dependencies
------------

No dependencies as of yet

Example Playbook
----------------

    - hosts: servers
      roles:
      - role: auto-deply-node-app
        vars:
          repo_url: git@github.com:gituser/Simple-Node-App.git
