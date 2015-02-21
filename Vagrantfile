# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.require_version '>= 1.5.1'

# IP Address for the host only network, change it to anything you like
# but please keep it within the IPv4 private network range
ip_address = "192.168.50.5"

# The project name is base for directories
# Will also be the hostname for your project (e.g.: http://projectname.local)
project_name = "vagrant.dev"

Vagrant.configure(2) do |config|
    config.vm.box = "ubuntu/trusty64"

    config.vm.network :private_network, ip: ip_address
    config.vm.hostname = project_name

    # Provision using Ansible
    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "./build.yml"
        ansible.inventory_path = "./hosts/local"
        ansible.limit = 'all'
    end

    config.vm.synced_folder "../../code/becomeadrivinginstructorhq.co.uk", "/srv/www/becomeadrivinginstructorhq.dev",
    owner: "drivinginstructor", group: "drivinginstructor"

    config.vm.synced_folder "../../code/selfemployedcourier.net", "/srv/www/selfemployedcourier.dev",
    owner: "selfemployedcourier", group: "selfemployedcourier"

    config.vm.synced_folder "../../code/proudlypowered.com", "/srv/www/proudlypowered.dev",
    owner: "proudlypowered", group: "proudlypowered"

    config.vm.synced_folder "../../code/thevamoose.com", "/srv/www/thevamoose.dev",
    owner: "thevamoose", group: "thevamoose"

    config.vm.synced_folder "../../code/magento.dev", "/srv/www/magento.dev",
    owner: "magento", group: "magento"

    config.vm.synced_folder "../../code/wordpress.dev", "/srv/www/wordpress.dev",
    owner: "wordpress", group: "wordpress"

    config.vm.synced_folder "../../code/prestashop.dev", "/srv/www/prestashop.dev",
    owner: "prestashop", group: "prestashop"

    config.vm.synced_folder "../../code/docnet.dev", "/srv/www/docnet.dev",
    owner: "docnet", group: "docnet"

    config.vm.synced_folder "../../code/zend.dev", "/srv/www/zend.dev",
    owner: "zend", group: "zend"

    if !Vagrant.has_plugin? 'vagrant-hostsupdater'
        puts 'vagrant-hostsupdater missing, please install the plugin:'
        puts 'vagrant plugin install vagrant-hostsupdater'
    else
        # If you have multiple sites/hosts on a single VM
        # uncomment and add them here
        config.hostsupdater.aliases = %w(becomeadrivinginstructorhq.dev selfemployedcourier.dev thevamoose.dev proudlypowered.dev magento.dev wordpress.dev prestashop.dev docnet.dev zend.dev)
    end

    # Fix for slow external network connections
    config.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    end
end
