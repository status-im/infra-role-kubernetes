# Description

This Role help to manage and setup a Kubernetes node.
It can be use to:
* Install a node
* Upgrade a node

# Installation

Installation is the default mode configured by `k8s_action: install`

## Master Node

To install a master node, run this role with the settings:
```yaml
kubernetes_is_master: True
```

## Workers

To install a worker, a cluster token must be generated with `kubeadm token create --print-join-command`

```bash
kubeadm token create --print-join-command
kubeadm join ${master_ip}:{master_port} --token ${some_token} --discovery-token-ca-cert-hash ${sha256}
```

```yaml
k8s_ca_cert_hashes: '${token}'
k8s_cluster_token: '${hash}'
```


### Firewall configuration

The deployement should, have the following config:
```
open_ports_list:
  kubernetes:
    - { source: '192.168.0.0/16', comment: 'Allow trafic from Pod Network'   }
    - { dest: '192.168.0.0/16',   comment: 'Allow trafic to Pod Network'     }
    - { source: '172.16.0.0/12',  comment: 'Allow trafic to Service Network' }
    - { dest: '172.16.0.0/12',    comment: 'Allow trafic to Service Network' }
 ```
 In case of a Master node, the port `6443` should be open also:
 ```
   kube-api-server:
    - { port: '6443', iifname: 'wg0', ipset: 'bi.test', comment: 'Access for Nodes to join master'}

```

## Upgrade

Instruction to upgrade a node can be found [here](./UPGRADE.md)
