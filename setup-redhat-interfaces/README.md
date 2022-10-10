Role Name
=========

Role to deploy standard network configuration

- Bonding
- NICs
- Routing

Requirements
------------

- device names
- mac addresses
- bond config
- ip
- netmask
- gateway
- routing information

Role Variables
--------------



All bond devices configured under bond_devices:

eth_opts is optional

```
bond_devices:
    - device: ens1f0
      mac: 98:f2:b3:dd:60:18
      master: mgt
      eth_opts: '-C ${DEVICE} adaptive-rx off rx-usecs 0 rx-frames 0; -K ${DEVICE} lro off'
    - device: ens1f1
      mac: 98:f2:b3:dd:60:19
      master: mgt
      eth_opts: -C ${DEVICE} adaptive-rx off rx-usecs 0 rx-frames 0; -K ${DEVICE} lro off
    - device: mgt
      ip: 10.61.12.20
      nm: 255.255.255.0
      gw: 10.61.12.1

```
Individual NICs under nic_devices:

```
nic_devices:

    - device: mgt_nic
      ip: 10.61.12.20
      nm: 255.255.255.0
      gw: 10.61.12.1
      mac: 98:f2:b3:dd:60:19
```

Routing information can be configured under group_vars for a group of hosts or on individual hosts

Under routes

```
routes:
    - device: mgt
      gw: 10.61.12.1
      route:
        - 0.0.0.0
        - 1.1.1.1
        - 2.2.2.2
    - device: app
      gw: 0.0.0.1
      route:
        - 1.2.3.4
```


Dependencies
------------

None

Example Playbook
----------------

Install from the requirements file

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: setup-network }

License
-------

BSD

Author Information
------------------

