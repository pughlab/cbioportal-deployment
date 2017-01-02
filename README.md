## cbioportal-deployment

This package contains [ansible](https://www.ansible.com/) plays for deploying a cBioPortal instance on a remote server.

### Inventories

To make managing multiple sites possible, a range of deployments can be managed
under a single directory, `inventories`. Each is a directory containing a `hosts.ini`
file and a `group_vars` directory containing the settings needed for each group.
All roles and deployments share settings. The variables can also be secured using
`ansible-vault`.

### With virtualbox

This is demonstrated by `inventories/virtualbox/hosts.ini`.

These groups use a config like this from .ssh/config. I assume you have an ssh
key set up accordingly.

    Host virtualbox
      RSAAuthentication yes
      HostName 127.0.0.1
      IdentityFile ~/.ssh/virtualbox_rsa
      User root
      Port 2228

The command is then:

    $ ansible-playbook -v -i inventories/virtualbox/hosts.ini provisioning.yml

### Overview

This deploys a complete and working cBioPortal. It also contains an import play which can be used
to add new data to the portal automatically.

### Importing data

You can also use this project to manage importing, using the playbook `import.yml`.

The command is:

    $ ansible-playbook -v -i inventories/virtualbox/hosts.ini --extra-vars="import_directory=..." import.yml
