## Warning: those playbooks works on my TEST cluster! 
## Use them at your own risk.

My kubernetes related ansible playbooks

**build.yml**

This playbook assumes you have latest rke installed
```
$ rke --version
rke version v1.3.12
$ rke config --list-version --all
v1.19.16-rancher1-6
v1.20.15-rancher1-4
v1.21.13-rancher1-1
v1.23.7-rancher1-1
v1.22.10-rancher1-1
v1.18.20-rancher1-3
```
Use the version of Kubernetes that suits you under `var:`

Make this playbook executable `chmod +x build.yml` and run it: `./build.yml`

This playbook will build kubernetes cluster, installs cert-manager and Rancher. Config file is generated from jinja2 (conf_template.j2) template.

Define your variables in **build.yml** file, add more master and/or worker nodes. If you need to **add new nodes after first run**, add nodes under `vars:` and run **build.yml** playbook again.

Define your cluster name and hostname. Hostname can't be IP address.

To use **kubectl** copy kube_config_<YOUR_HOSTNAME>.yml to ~/.kube/config
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

Copy your *.rkestate to cluster.rkestate

**cluster.yml**

my testcluster setup.

**hosts**

Contains my hosts list.
