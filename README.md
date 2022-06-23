## Warning: those playbooks works on my TEST cluster! 
## Use them at your own risk.

My kubernetes related ansible playbooks

**build.yml**

This playbook will build kubernetes cluster, installs cert-manager and Rancher.

Define your variables in that file, add more master and/or worker nodes.

Define your cluster name and hostname. Hostname can't be IP address.

To use kubectl copy kube_config_<YOUR_HOSTNAME>.yml to ~/.kube/config
```
$ cp kube_config_hostname.com.yml ~/.kube/config 
$ kubectl get nodes
NAME             STATUS   ROLES               AGE   VERSION
192.168.122.14   Ready    controlplane,etcd   14m   v1.23.7
192.168.122.15   Ready    worker              14m   v1.23.7
```

**kube_drain.yml**
Drains kubernetes nodes, which are described in hosts file. workers first, then etcd-cp nodes in serial, one by one.
Upgrades node, restarts if needed and makes it schedulable again.

**kube_upgrade.yml**
Downloads latest RKE version, gets latest available kubernetes version and upgrades nodes with: rke up --config cluster.yml

**cluster.yml**
my testcluster setup.

**hosts**
Contains my hosts list.
