# Ansible role: bird
BGP dynamic routing engine.
Used for routing on wireguard VPN with unreliable nodes.

## Requirements
Only tested on Debian stable, for now.

## Role Variables
+ `bgp_iface` (default: `ansible_default_ipv4`): interface to listen on.
+ `bird_ip` (default: `ansible_default_ipv4`): local IP to identify host.
+ `bird_conf`: contents for `/etc/bird/bird.conf` (multiline string).
+ `bird_bgp_neighbors`: list of dict (name, template, neighbors).
  `neighbors` should be a dict of (name, IP) pairs.
  Iterates over the given list of neighbors, generating protocol stanzas
  referencing the given template and changing only the neighbor IP.

## Usage Examples
### Generating protocols from a list of neighbors
This demonstrates the use of `bird_bgp_neighbors`:

```
bird_conf: |
  template bgp peer {
    local as my_as;
    neighbor as my_as;
  }

bird_bgp_neighbors:
- name: peer_bgp
  template: peer
  neighbors:
    peer1: 192.168.1.1
    peer2: 192.168.1.2
    peer3: 192.168.1.3
```

### Assembling multiline config
It is recommended to define `bird_conf` by combining multiple host vars:

```
bird_conf_00: |
  log syslog all;
  define my_as 65000;
bird_conf_05_kernel: |
  protocol kernel {
    ipv4 {
      export where source = RTS_BGP;
    }
  }

bird_conf: "{{ q('varnames', '^bird_conf_') | sort | 
  map('extract', vars) | join('\n') }}"
```

This enables inventory groups and invididual hosts to override portions of the config.

## Playbooks
+ `main.yml`: apply role
+ `uninstall.yml`: remove. Run prior to removing host from inventory group.

## Dependencies
None.

## License
+ Ansible role licensed [MIT](LICENSE)

## Author Information
+ [Bird](https://bird.network.cz/)
+ Ansible role by [Sean Ho](https://github.com/ho-ansible/)
