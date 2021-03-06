# Kubernetes cluster installation

This set of Ansible roles creates a fully operational cluster from scratch. At least two Debian-based machines with base settings are needed. The machine running this Playbook needs to have ssh access to those servers.

The required system settings, the ssh access between all nodes with auto generated keys will be set up and Docker will be installed. Then a Kubernetes cluster will be set up with [RKE](https://rancher.com/docs/rke/latest/en/).

Also a distributed block storage system [Longhorn](https://github.com/longhorn/longhorn) and the [Cert-Manager](https://github.com/jetstack/cert-manager) will be added if you enable this options in the host vars for the admin node.

# Run

Set up your inventory. The easiest way is to copy the [example inventory](inventories/test) and to fill it with your values. 

To build the cluster run:

```
ansible-playbook -i <YOURINVENTORY> kubernetes.yml
```

# Tests

[Ansible Molecule](https://github.com/ansible-community/molecule), [Molecule-Vagrant](https://github.com/ansible-community/molecule-vagrant), [Vagrant](https://github.com/hashicorp/vagrant) and [VirtualBox](https://www.virtualbox.org/) need to be installed to build the cluster locally and to start the tests.

```
sudo apt install virtualbox vagrant python3-pip
pip3 install molecule
pip3 install molecule-vagrant
```

Ansible Molecule has been "misused" in this project. Normally used to test single Ansible roles,
it is used to test the whole playbook here.

The cluster will be started and tested locally with Ansible Molecule. Simply run `molecule converge`
to start a cluster with 3 master and 3 worker nodes and to install the Kubernetes cluster.
The local public ssh key (`~/.ssh/id_rsa.pub`) will be added to each machine
(login user is 'vagrant').

Tests  can be started with `molecule verify` (the local cluster, installed with
`molecule converge` will not be destroyed) or with `molecule test` (the existing local
cluster will be destroyed if it exists, tests and lints will be made and the cluster
will be cleaned up afterwards).
