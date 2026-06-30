# Kubernetes upgrade

This role can be used to upgrade the a kubernetes cluster.

> Kubernetes upgrade need to be done one version after the other. Don't jump 2 versions.

## Requirements

Before any execution, ensure the backup of the ETCD instance and any application are up to date.

To run correctly the role must be run with the varaible `k8s_action` to `upgrade` and `k8s_upgrade_version` to the version aimed for the upgrade, example `1.36`

## Execution

This part of the role will execute the tasks in `tasks/upgrade/main.yml`, they will:
* Upgrade the kubeadmin package
* Prepare an upgrade plan
* Ask for confirmation
* Run the kubeadmin upgrade
* Drain the node to avoid new pods deployement
* Upgrade the kubelet and kubectl package
* Restart the kubelet Service
* Uncordon the node.

## Sources

* [Control Plane upgrade](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)
* [Node upgrade](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/upgrading-linux-nodes/)
