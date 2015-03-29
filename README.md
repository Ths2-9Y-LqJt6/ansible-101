This is just a quick and dirty Ansible 101 for interacting with Linux servers.

#Installing Ansible

Via PIP, this will get Ansible up and running on your machine:

```
pip install ansible
```

This should also install dependencies, including paramiko, PyYAML, and Jinja2.

You can install Ansible other ways, but I recommend installing via PIP so you can take advantage of any python packages installed by PIP.

#Getting Started

Create an /etc/ansible/hosts file. This will allow you to group hosts together with a group name. For example, your /etc/ansible/hosts file might look like:

```
[local]
localhost

[test]
# debian1
100.42.00.10
# debian2
100.42.00.11
# debian3
100.42.00.12
```

Time to try your first Ansible command:

```
ansible test -m ping -u root -k
```

When you run a playbook, you can specify which group to run that command or playbook on. For the command, just specify in the command itself (such as the example above). In playbooks, you can specify the host either in the playbook itself (i.e., hosts: <$hostgroup> as the first item in the playbook) or by limiting it when you run the playbook:

```
ansible-playbook -l <$hostgroup_or_name> playbook.yml
```

By default, Ansible assumes using ssh keys for keyless access. To override that behavior:

```
-u <$username> #overrides the remote username (default: your current username)
-k #prompts for SSH password
```

#Roles
Roles are an built-in structured way to organize templates, variables, and tasks in Ansible.

* roles
 * <$role_name>
  * templates
   * <$myTemplate>.j2
  * tasks
   * main.yml
  * vars
   * main.yml

Each <$role_name> can be whatever you want it to be, but the underlying structure should be the same. You can have multiple tasks and vars .yml files, and simply include them in the main.yml file and Ansible will incorporate them automatically when it runs.
