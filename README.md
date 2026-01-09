# Description

Role to deploy a Kubernetes node

# Usage

## Master Node

To install a master node, run this role with the settings:
```yaml
kubernetes_is_master: True
```

## Workers

To install a worker, it need:
```yaml
kubernetes_admin_ip: '10.0.0.2'
kubernetes_worker_join_command: ''
```

