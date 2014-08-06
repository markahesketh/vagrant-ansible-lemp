# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
    # Every Vagrant virtual environment requires a box to build off of.
    config.vm.box = "ubuntu/trusty64"

    # Create a private network, which allows host-only access to the machine
    # using a specific IP.
    config.vm.network "private_network", ip: "192.168.33.10"

    # Provision using Ansible
    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "provision.yml"
    end

    config.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    end
end
