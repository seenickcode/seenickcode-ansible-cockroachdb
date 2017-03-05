# Introduction

This is an Ansible example for spinning up an insecure CockroachDB cluster for servers hosted on AWS.  For example purposes only, not for production use. Thanks to Mikael Sandström, @oravirt for his example code at https://github.com/oravirt/ansible-cockroachdb

# Setup

1. Spin up 3 AWS EC2 instances with Ubuntu 16.04
2. Create an AWS Security Group to be used by each instance, allowing ports 8080, 26257 as applicable.
3. Create your own <environment>.ini file using the server.ini.template file provided and the new AWS instance public/private IPs created.
4. Edit ``cockroach-db/defaults/main.yml`` to configure the database names you'd like to create.
5. Run ``ansible-playbook install-cockroachdb.yml -i <your .ini file>``.  This will spin up a cluster, setting the appropriate databases.

# Example Use

```
ansible-playbook install-cockroachdb.yml -i staging.ini
```

# Gotchas

1. Because we're using private IPs to spin up each instance, if SSH'd into a server, always pass the ``--host=<private IP>`` even if it refers to localhost.

# Cheat Sheet

- running a random command: ``ansible cdb-01 -i staging.ini -m ping -e 'ansible_python_interpreter=/usr/bin/python3'``
- looking at host vars of a specific server: ``ansible -m debug cdb-01 -a 'var=hostvars' -i staging.ini``

# Best Practices

- http://docs.ansible.com/ansible/playbooks_best_practices.html#directory-layout

# Credits

Thanks to Mikael Sandström, @oravirt for his Ansible modules and role examples. Those role examples were tweaked to work with AWS.

# To Do

- [ ] Prevent need to use a mix of public and private IPs. For some reason instances can't be started using AWS public IPs.