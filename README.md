# Ansible role: bird
BGP dynamic routing engine.
Used for routing on wireguard VPN with unreliable nodes.

## Requirements
Only tested on Debian stable, for now.

## Role Variables
+ `bird_conf`: Contents of `/etc/bird/bird.conf` as a multiline string.
+ `bgp_port` (default: 179): TCP port to open on firewall

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
