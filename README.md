Ansible Role OpenVPN
=========

This role installs and configures OpenVPN Server/Client on Ubuntu 20.04+.

Requirements
------------

Operating System Support: Ubuntu 20.04 or later

Role Variables
--------------

### Server
```
ovpn_mode: server
ovpn_server_service_port: "119{{ ovpn_server_tunnel_number }}"
# ovpn_server_tunnel_local_address: 192.168.100.{{ ovpn_server_tunnel_number|int * 2 -1 }}
# ovpn_server_tunnel_remote_address: 192.168.100.{{ ovpn_server_tunnel_number|int * 2 }}
ovpn_server_tunnel_key_download_path: "{{ lookup('env', 'HOME') }}/ansible_openvpn/tunnel_keys"
ovpn_server_public_interface: "{{ ansible_default_ipv4['interface'] }}"
# ovpn_server_tunnels:
#   - tunnel_number: 1
#     client_alias: client1
#     client_source_ip_address: 192.168.64.10
```

### Server - UFW
```
ovpn_ufw_default_route_policy: allow
ovpn_ufw_deny_routed_traffic_from_untrusted_interfaces: true
ovpn_untrusted_interfaces:
  - "{{ ansible_default_ipv4['interface'] }}"
```

### Client
```
ovpn_mode: client
# ovpn_client_tunnel_number: 1
# ovpn_client_server_tunnel_number: ""
# ovpn_client_server_hostname: ""
# ovpn_client_server_address: ""
ovpn_client_server_service_port: 119{{ ovpn_client_server_tunnel_number }}
ovpn_client_server_tunnel_key_local_path: "{{ lookup('env', 'HOME') }}/cynetwork_openvpn/tunnel_keys"
# ovpn_client_tunnel_local_address: 192.168.100.{{ ovpn_client_server_tunnel_number|int * 2 }}
# ovpn_client_tunnel_remote_address: 192.168.100.{{ ovpn_client_server_tunnel_number|int * 2 -1 }}
# ovpn_client_tunnels:
#   - tunnel_number: 1
#     server_hostname: server1
#     server_tunnel_number: 11
```

Dependencies
------------

No dependency.

Example Playbook
----------------

Install
```
ansible-galaxy install cihanyilmazer.ansible_role_openvpn
```

    - hosts: servers
      roles:
         - cihanyilmazer.ansible_role_openvpn/server
         
    - hosts: client
      roles:
         - cihanyilmazer.ansible_role_openvpn/client

License
-------

MIT

Author Information
------------------

Cihan Yilmazer<br />
https://www.cihanyilmazer.com<br />
https://www.github.com/cihanyilmazer<br />
https://galaxy.ansible.com/cihanyilmazer<br />