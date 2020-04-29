Install Mongo DB
=========

This role installs the latest mongodb on Debian or RedHat families.

Role Variables
--------------

Currently this role installs the latest verison. Might add some variables so that users can install any specific version.

Example Playbook
----------------

    - hosts: servers
      roles:
      - install-mongodb
