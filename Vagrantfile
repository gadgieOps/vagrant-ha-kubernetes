# -*- mode: ruby -*-
# vi: set ft=ruby :

IMAGE = "bento/ubuntu-20.04"
#IMAGE = "bento/centos-7.9"

###
# CONTROLLER_N: 1-3
#
CONTROLLER_N = 3

###
# WORKER_N: 0-3
#
WORKER_N = 3

Vagrant.configure("2") do |config|

  config.vm.provider "virtualbox" do |vb|
     vb.gui = false
     vb.memory = "2048"
  end

  ###
  #  Control
  #

  (1..CONTROLLER_N). each do |i|
    config.vm.define "control-#{i}" do |control|
      control.vm.box = IMAGE
      control.vm.hostname = "control-#{i}"
      control.vm.network "private_network", ip: "192.168.60.10#{i}"

      # Start provisioning when last VM is launched and there are no configured workers
      if i == CONTROLLER_N && WORKER_N == 0
        control.vm.provision "ansible" do |ansible|
          ansible(ansible)
      end
    end
  end
end

  ###
  #  Workers
  #

  if WORKER_N > 0
    (1..WORKER_N). each do |i|
      config.vm.define "worker-#{i}" do |worker|
        worker.vm.box = IMAGE
        worker.vm.hostname = "worker-#{i}"
        worker.vm.network "private_network", ip: "192.168.60.11#{i}"

        # Start provisioning when last VM is launched
        if i == WORKER_N
          worker.vm.provision "ansible" do |ansible|
            ansible(ansible)
          end
        end
      end
    end
  end
end

###
# Provision Instructions
#

def ansible (v)
  v.playbook = "playbooks/provision-cluster.yml"
  v.inventory_path = "inventories/nodes.yml"
  v.limit = "all"
end
