# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.synced_folder ".", "/vagrant"
  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
  end
  config.vm.define :dev do |d|
    d.vm.network "public_network", bridge: "eno4", ip: "192.168.57.35", auto_config: "false", netmask: "255.255.255.0" , gateway: "192.168.57.1"
    d.vm.provision "shell", path: "bootstrap.sh"
    d.vm.provision :shell, inline: 'ansible-playbook /vagrant/ansible/dev.yml -c local -v'
    d.vm.hostname = "books-fe-polymer-dev"
  end
  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end
end