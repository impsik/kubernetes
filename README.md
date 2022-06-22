# kubernetes
kubernetes related ansible playbooks

## kube_drain.yml
Drains kubernetes nodes, which are described in hosts file. workers first, then etcd-cp nodes in serial, one by one.

## kube_upgrade.yml
Downloads latest RKE version, gets latest available kubernetes version and upgrades nodes with: rke up --config cluster.yml

## cluster.yml 
my testcluster setup.
