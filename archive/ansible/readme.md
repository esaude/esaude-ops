<br/><br/><br/>
<img src="https://s3-eu-west-1.amazonaws.com/esaude/images/esaude-site-header.png" alt="OpenMRS"/>
<br/><br/><br/>

# eSaude Infrastructure Ansible Playbooks

Ansible is a tool to run `playbooks` for machines of a certain `inventory`. Each
machine in an inventory can belong to several different groups. You can
configure global variables (an special group called `all`), per group or per
host.

## Running ansible
The following assumes you are in the `ansible` directory:

```
# Download all roles/modules
$ ansible-galaxy install -p roles -r requirements.yml --force

# Run ansible in a specific machine
$ ansible-playbook -i inventories/all -l ship.esaude.org -u <YOUR USERNAME> site.yml

# Do a test run without actually applying the playbook
$ ansible-playbook -i inventories/all -l ship.esaude.org -u <YOUR USERNAME> site.yml --check

# Run on all machines
$ ansible-playbook -i inventories/all -u <YOUR USERNAME> site.yml

# Run arbitrary code
$ ansible -i inventories/production -m "whoami"
```
