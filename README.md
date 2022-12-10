Vagrant: Build a highly available kubernetes cluster
=========
Vagrant project to spin up a local highly available kubernetes cluster for development and testing purposes. See https://github.com/gadgieOps/ha-kubernetes.git for further information on the underlying ansible code.

Dependencies
------------

Required roles:
- gadgieOps.ha-kubernetes

Can be installed using:
~~~
ansible-galaxy install -r requirements.yml
~~~

Usage
-----

1. In the Vagrantfile
    - Set CONTROLLER_N to specify the number of control plane nodes to spin up
    - Set WORKER_N to specify the number of worker nodes to spin up
2. Modify inventories/nodes.yml to match the quantities of nodes
    - It may be simpler to comment out any unrequired nodes
3. Customize role vars in playbooks/provision-cluster.yml for further information
    - See https://github.com/gadgieOps/ha-kubernetes.git
4. Use 'vagrant up' to spin up the cluster
5. Use 'vagrant halt' to turn off the cluster
6. Use 'vagrant destroy' to destroy the cluster

Collaboration
-------------
Please feel free to raise issues and submit pull requests. I have been using this role along side Vagrant to spin up dev and test environments that are in line with my production environment. I am working on making this role more generic and accessible for other usecases.

Notes
-----
Tested using:
- Ubuntu 20.04
- CentOS 7.9

License
-------
MIT

Author Information
------------------
Authored by gadgieOps.
