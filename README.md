# Ansible role: bird
BGP dynamic routing engine.
Used for routing on wireguard VPN with unreliable nodes.

## Requirements
Only tested on Debian stable, for now.

## Role Variables
+ `bgp_iface` (default: `ansible_default_ipv4`): interface to listen on.
+ `bird_id` (default: `ansible_default_ipv4`): 
  ID to use in config, usually public IP.
+ `bird_config`: extra contents for `/etc/bird/bird.conf` (multiline string).
+ `bird_protocol_*` (e.g., `bird_protocol_bgp_mybgp`): 
  multiline string defining a single protocol stanza.
  The protocol type and name are taken from the variable name.
+ `bird_template_*`: same for templates
+ `bird_filter_*`: same for filters

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
