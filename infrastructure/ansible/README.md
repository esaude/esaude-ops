# Ansible

## [About](http://docs.ansible.com/ansible/#about-ansible)

For quick and lazy introduction, check out the [Quick Start Video](https://www.ansible.com/quick-start-video).

Ansible is an IT automation tool. It can configure systems, deploy software,
and orchestrate more advanced IT tasks such as continuous deployments or zero downtime rolling updates.

Ansible’s main goals are simplicity and ease-of-use. It also has a strong focus on security and reliability,
featuring a minimum of moving parts, usage of OpenSSH for transport,
and a language that is designed around auditability by humans–even those not familiar with the program.

We believe simplicity is relevant to all sizes of environments, so we design for busy users of all types:
developers, sysadmins, release engineers, IT managers, and everyone in between.
Ansible is appropriate for managing all environments, from small setups with a handful of instances
to enterprise environments with many thousands of instances.

Ansible manages machines in an agent-less manner.
There is never a question of how to upgrade remote daemons or the problem of not being able to manage systems
because daemons are uninstalled.
Because OpenSSH is one of the most peer-reviewed open source components, security exposure is greatly reduced.

## [Getting Started](http://docs.ansible.com/ansible/index.html)

1. [Installation (Ubuntu)](http://docs.ansible.com/ansible/intro_installation.html#latest-releases-via-apt-ubuntu)
**NB!** Ansible need only be installed on the control machine and not on the servers.

1. Check out [Inventory](http://docs.ansible.com/ansible/intro_inventory.html) and
[Playbooks](http://docs.ansible.com/ansible/playbooks.html) for help understanding the relevant building blocks.

1. Check out [Roles](http://docs.ansible.com/ansible/playbooks_roles.html#roles) to understand how the files are
organised and where to find/put what.

1. Running our playbooks: **NB!** With great power comes great responsibility! When in doubt, call for backup.
Ensure that you have tested any changes against a test or staging server before running against any production servers.

General usage: `$ ansible-playbook playbook.yml`

Useful flags:
* -i INVENTORY, --inventory-file=INVENTORY
                          specify inventory host path
                          (default=/etc/ansible/hosts) or comma separated host
                          list.
* --list-hosts          outputs a list of matching hosts; does not execute
                        anything else
* -C, --check           don't make any changes; instead, try to predict some
                        of the changes that may occur
* -u REMOTE_USER, --user=REMOTE_USER
                        connect as this user (default=None)
* -b, --become        run operations with become (does not imply password
                        prompting)
* -K, --ask-become-pass
                        ask for privilege escalation password

To run a playbook you should do:

```bash
ansible-playbook \
  --ask-vault-pass \
  --become \
  --inventory=inventories/qa \
  --user=deploy \
  playbooks/deploy_epts_qa.yml
```

If you are configuring the servers for the first time you will need to use the `root` user and can remove the `--become` flag. You will need to manually SSH into the servers and allow the SSH connection before the deploy script will run successfully.

## Vault

The vault password required for running the playbooks can be found in the MOASIS KeePass file.

To encrypt a new secret with vault run:

```bash
echo -n '<YOUR SECRET>' | ansible-vault encrypt_string
```