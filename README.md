# Full Kubernetes cluster installation

Following will be installed / configured with 
`ansible-playbook -i inventory/test kubernetes.yml`:
* The base system
* SSH access between all nodes with auto generated SSH keys
* Docker
* Kubernetes cluster (with "RKE")
* Distributed block storage system "Longhorn"
* Certificate manager

This installation works only on Debian-based systems.

It is needed to fill the hosts file in the existing test-invetory or to create
a own one.

# Tests

Molecule, Vagrant and VirtualBox need to be installed to build the cluster
locally and to start the tests.

Molecule has been misused in this project. Normally used to test single Ansible roles,
it is used to test the whole playbook here.

The cluster will be started and tested locally with molecule. Simply run `molecule converge`
to start a cluster with 3 master and 3 worker nodes and to install the Kubernetes cluster.
The local public ssh key (`~/.ssh/id_rsa.pub`) will be added to each machine
(login user is 'vagrant').

Tests  can be started with `molecule verify` (the local cluster, installed with
`molecule converge` will not be destroyed) or with `molecule test` (the existing local
cluster will be destroyed if it exists, tests and lints will be made and the cluster
will be cleaned up afterwards).