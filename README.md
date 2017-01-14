## cbioportal-deployment

This package contains [ansible](https://www.ansible.com/) plays for deploying a
cBioPortal instance on a remote server.

The repository also contains an import play which can be used to add new data
to the portal automatically.

### Inventories

To make managing multiple sites possible, a range of deployments can be managed
under a single directory, `inventories`. Each is a directory containing a `hosts.ini`
file and a `group_vars` directory containing the settings needed for each group.
All roles and deployments share settings.

### Security

The `group_vars` files are encrypted using `ansible-vault`, so data in these
files can be committed. The vault password is kept in a separate file,
`.vault-password`, and configured so that it is read automatically when
needed (using `ansible.cfg`).  Obviously, `.vault-password` should *never* be
committed to version control. It doesn't even need to exist, and can be
given manually by prompt if needed.

To encrypt and decrypt these files, use a command like:

    $ ansible-vault decrypt inventories/oicr/group_vars/all
    $ ansible-vault encrypt inventories/oicr/group_vars/all

This makes maintenance a little clunkier than managing everything locally, but
does provide a backup for all the settings. And nothing should be directly
accessible anyway, as ssh keys are there to secure connections to the
servers.

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

    $ ansible-playbook -i inventories/virtualbox/hosts.ini provisioning.yml

### Importing data

You can also use this project to manage importing, using the playbook `import.yml`.

The command is:

    $ ansible-playbook -v -i inventories/virtualbox/hosts.ini --extra-vars="import_directory=..." import.yml
