This is just a quick and dirty Ansible 101 for interacting with Linux servers.

#Installing Ansible

Via PIP, this will get Ansible up and running on your machine:

```
pip install -r paramiko PyYAML Jinja2 httplib2 ansible
```

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

Now, when you run a playbook, you can specify which group to run that playbook on either in the playbook itself (i.e., hosts: <$hostgroup> as the first item in the playbook) or by limiting it when you run the playbook:

```
ansible-playbook -l <$hostgroup_or_name> playbook.yml
```

By default, Ansible assumes using ssh keys for keyless access. To override that behavior:

```
-u #overrides the remote username (default: your current username)
-k #prompts for SSH password
```
