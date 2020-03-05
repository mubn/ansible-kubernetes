# Full Kubernetes cluster installation

Following will be installed / configured with 
`ansible-playbook -i inventory/test kubernetes.yml`
(hosts in the `hosts`-file or a whole own inventory needs to be created):
* The base system
* SSH access between all nodes
* Docker
* The Kubernetes cluster (with "RKE")
* Distributed block storage system "Longhorn"
* Certificate manager

It works only on Debian-based systems.

# Tests

The cluster can be started locally with molecule. Simply run `molecule converge`
to set up a cluster with 3 master and 3 worker nodes and to install the Kubernetes
(molecule and vagrant need to be installed on the host) cluster.
The local public ssh key (`~/.ssh/id_rsa.pub`) will be added to each machine
(login user is 'vagrant').

Todo:

* Testinfra tests (`molecule verify` / `molecule test`)
