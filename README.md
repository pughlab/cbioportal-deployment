## cbioportal-deployment

This package contains [ansible](https://www.ansible.com/) plays for deploying a cBioPortal instance on a remote server.

### With virtualbox

This is demonstrated by `test-inventory.ini`.

These groups use a config like this from .ssh/config. I assume you have an ssh
key set up accordingly.

    Host virtualbox
      RSAAuthentication yes
      HostName 127.0.0.1
      IdentityFile ~/.ssh/virtualbox_rsa
      User root
      Port 2228

The command is then:

    $ ansible-playbook -vv -i test-inventory.ini provisioning.yml

### Overview

This deploys a complete and working cBioPortal. It also contains an import play which can be used
to add new data to the portal automatically.
