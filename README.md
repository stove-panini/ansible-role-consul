consul (WIP)
======
Deploys HashiCorp Consul servers and clients.

This role bootstraps a cluster just fine, but I need to dig into the other features like Consul Connect and Snapshots

Dependencies
============
[hashicorp-repo](https://github.com/stove-panini/ansible-role-hashicorp-repo)

Role Variables
--------------
| Name | Default Value | Comment |
| ---- | ------------- | ------- |
| consul\_state | `present` | |
| consul\_version | `""` | By default, we just insure that Consul is installed |
| consul\_servers\_group | `consul_servers` | Ansible inventory group containing the server node(s) |
| consul\_configure\_firewalld | `true` | |
| consul\_force\_bootstrap | `false` | Force the reinitialization of the cluster |
| consul\_common\_configuration | `{}` | |
| consul\_server\_configuration | `{}` | See below |
| consul\_client\_configuration | `{}` | |

The `consul_*_configuration` variables are merged with their respective `consul_*_configuration_defaults` variable found in the `vars/` directory. You should structure these exactly as you would the resulting JSON config file. See the [official docs](https://www.consul.io/docs/agent/options) for available options.

Example Playbook
----------------
``` yaml
- hosts: consul_cluster
  roles:
    - role: consul
      vars:
        consul_version: 1.11.2
        consul_server_configuration:
          ui_config:
            enabled: true
```
