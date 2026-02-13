# Description

Role to deploy a Kubernetes node

# Usage

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
