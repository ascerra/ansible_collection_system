[![Build Status](https://travis-ci.org/oasis-roles/firewalld.svg?branch=master)](https://travis-ci.org/oasis-roles/firewalld)

ROLE NAME
===========

This role provides basic hole punching and local port forwarding for the
firewalld service, to aid in the task of running application stacks deployed
using the OASIS roles.  It provides a simple interface to the Ansible
[firewalld
module](https://docs.ansible.com/ansible/latest/modules/firewalld_module.html).

Requirements
------------

Ansible 2.4 or higher

Red Hat Enterprise Linux 7 or equivalent

Valid Red Hat Subscriptions

Role Variables
--------------

Currently the following variables are supported:

### General

* `firewalld_zone` - firewall zone for all rules
* `firewalld_ports_open` - permanently open ports (IPv4+IPv6) for given
  firewall zone
* `firewalld_ports_forward` - permanently forward local ports (IPv4+IPV6) for
  given firewall zone, e.g. TCP 80->8080 for webapps

Dependencies
------------

None

Example Playbook
----------------

```
- hosts: firewalld-servers
  roles:
    - role: firewalld
      firewalld_zone: public
      firewalld_ports_open:
        - proto: tcp
          port: 8080
        - proto: udp
          port: 9990-9999
      firewalld_ports_forward:
        - proto: tcp
          port: 80
          to_port: 8080
```

License
-------

GPLv3

Author Information
------------------

David Roble <droble@redhat.com>
