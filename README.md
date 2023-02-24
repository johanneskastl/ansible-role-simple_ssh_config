![Ansible Lint](https://github.com/johanneskastl/ansible-role-simple_ssh_config/workflows/Ansible%20Lint/badge.svg)

simple_ssh_config
=========

Create a simple ~/.ssh/config for a list of users

Requirements
------------

None.

Role Variables
--------------

```
- role: 'simple_ssh_config'
  list_of_users:
    - name: "{{ ansible_user }}"
      home: "/home/{{ ansible_user }}"
      list_of_hosts:
        - hostname_or_pattern: '10.250.2.*'
          strict_host_key_checking: 'yes'
          userknownhostfile: 'hosts_dmz'
    - name: 'deployer'
      home: "/deployer"
      list_of_hosts:
        - hostname_or_pattern: '10.250.2.*'
          strict_host_key_checking: 'accept-new'
          userknownhostfile: '/dev/null'
    - name: 'root'
      home: "/root"
      list_of_hosts:
        - hostname_or_pattern: '*'
          strict_host_key_checking: 'yes'
          userknownhostfile: 'known_hosts_root'
```

`list_of_users`: list of hashes, one for each user
The hash can contain a `name`, a path in `home`, and a list of hosts.

`list_of_hosts`: list of hashes, one for each target host.
The hash must currently contain the three attributes for each target host:
- `hostname_or_pattern`: hostname or pattern, e.g. `10.11.12.*`
- `strict_host_key_checking`: whether to check the host key (possible values see `man ssh_config`
- `userknownhostfile`: path to a knownhosts file (or /dev/null if you are sure you want to ignore and never check the host key)


Dependencies
------------

None

Example Playbook
----------------

    - hosts: servers
      roles:
         - role: 'johanneskastl.simple_ssh_config'

License
-------

BSD-3-Clause

Author Information
------------------

I am Johannes Kastl, reachable via kastl@b1-systems.de.
