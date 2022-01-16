`docker_macvlan_trunk`
=========

This will configure a macvlan-trunk-based network based on a parent trunk device.   `macvlan` has certain
limitations in addition to its advantages when in bridge mode so be sure to either understand what is being
accomplished here before making an attempt or else do so in a sandbox virtual network.

**Improper configuration can disrupt network connectivity both to the host
being configured as well as to all other hosts on the network to which it is
attached.**

See also [ansible-systemd-networkd-macvlan-trunk][1].


Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

### `iprange`

The range from which to auto-assign addresses for this docker host.  Ensure it doesn't overlap any real hosts
or else assign static IPs to each docker container.

### `gateway`

The gateway present on your local network.

### `subnet`

Your network's subnet.

### `network_name`

The network's name as it will be configured in docker.

### `parent`

The parent device for macvlan devices.

Dependencies
------------

There is no playbook dependency but the example uses my related `systemd_networkd_macvlan_trunk` for
ease of deployment.

Example Playbook
----------------

   - role: jamesandariese.systemd_networkd_macvlan_trunk
   - role: jamesandariese.docker_macvlan_bridge
     iprange: "192.168.1.240/28"
     gateway: "192.168.1.1"
     subnet: "192.168.1.0/24"
     network_name: trunk
     parent: trunk


License
-------

MIT

Author Information
------------------

Copyright 2022, James Andariese (first name at strudelline.net).


[1]: https://github.com/jamesandariese/ansible-systemd-networkd-macvlan-trunk
