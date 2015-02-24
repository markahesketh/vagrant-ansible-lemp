# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.require_version '>= 1.5.1'

# IP Address for the host only network, change it to anything you like
# but please keep it within the IPv4 private network range
ip_address = "192.168.50.5"

# The project name is base for directories
# Will also be the hostname for your project (e.g.: http://projectname.local)
hostname = "vagrant"

Vagrant.configure(2) do |config|
    config.vm.box = "ubuntu/trusty64"

    config.vm.network :private_network, ip: ip_address
    config.vm.hostname = hostname

    if !Vagrant.has_plugin? 'vagrant-hostsupdater'
        puts 'vagrant-hostsupdater missing, please install the plugin:'
        puts 'vagrant plugin install vagrant-hostsupdater'
    else
        # If you have multiple sites/hosts on a single VM
        # uncomment and add them here
        config.hostsupdater.aliases = %w(thevamoose.dev)
    end

    config.vm.synced_folder "~/Code/thevamoose.com", "/srv/www/thevamoose.dev",
    owner: "thevamoose", group: "thevamoose"

    # Provision using Ansible
    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "./build.yml"
        ansible.inventory_path = "./hosts/local"
        ansible.limit = 'all'
    end

    # Fix for slow external network connections
    config.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    end
end
