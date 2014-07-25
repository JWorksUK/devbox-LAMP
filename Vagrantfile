# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network :private_network, ip: "10.11.20.14"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.synced_folder ".", "/vagrant", :nfs => true
  config.vm.synced_folder "./site", "/var/www/site", :nfs => true
  config.vm.provision :ansible do |ansible|
    ansible.playbook = "devops/vagrant.yml"
    ansible.inventory_path = "devops/hosts"
    ansible.limit = 'vagrant'
    ansible.extra_vars = { ansible_ssh_user: 'vagrant',
                 ansible_connection: 'ssh',
                 ansible_ssh_args: '-o ForwardAgent=yes'}
  end
end
