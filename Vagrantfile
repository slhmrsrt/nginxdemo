# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/trusty64"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 22, host: 8022

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.hostname = "flaskapp"
  config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Set the name of the VM. See: http://stackoverflow.com/a/17864388/100134
  config.vm.define :flaskapp do |flaskapp|
  end
  
  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "./", "/var/www/"

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-add-repository -y ppa:ansible/ansible
    sudo apt-get update
    sudo apt-get install -y ansible
    sudo mkdir /etc/ansible/roles/nginxdemo
    sudo rsync -av --progress /var/www/ /etc/ansible/roles/nginxdemo/ --exclude Vagrantfile
    sudo rsync -av --progress /var/www/tests/flaskapp /home/vagrant/
    sudo /usr/bin/ansible-playbook -i /etc/ansible/roles/nginxdemo/tests/inventory /etc/ansible/roles/nginxdemo/tests/test.yml
  SHELL

  #config.vm.provision "ansible_local" do |ansible|
   #ansible.inventory_path = "/etc/ansible/roles/nginxdemo/tests/inventory"
   #ansible.playbook = "/etc/ansible/roles/nginxdemo/tests/test.yml"
   #ansible.verbose = "true"
  #end
end
