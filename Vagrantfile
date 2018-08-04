# encoding: utf-8
# -*- mode: ruby -*-
# vi: set ft=ruby :

# Box / OS
#VAGRANT_BOX = 'ubuntu/trusty64'
VAGRANT_BOX = 'debian/stretch64'

# Memorable name for your
VM_NAME = 'debian'

# VM User — 'vagrant' by default
VM_USER = 'vagrant'

# Username on your Mac
#MAC_USER = 'John'

# Host folder to sync
#HOST_PATH = '/Users/' + MAC_USER + '/' + VM_NAME

# Where to sync to on Guest — 'vagrant' is the default user name
#GUEST_PATH = '/home/' + VM_USER + '/' + VM_NAME

# # VM Port — uncomment this to use NAT instead of DHCP
VM_PORT = 2022
VM_PORT2 = 8080

Vagrant.configure(2) do |config|

  config.ssh.insert_key = false

  # Vagrant box from Hashicorp
  config.vm.box = VAGRANT_BOX
  
  # Actual machine name
  config.vm.hostname = VM_NAME

  # Set VM name in Virtualbox
  config.vm.provider "virtualbox" do |v|
    v.name = VM_NAME
    v.memory = 256
  end

  #DHCP — comment this out if planning on using NAT instead
  config.vm.network "private_network", type: "dhcp"

  # # Port forwarding — uncomment this to use NAT instead of DHCP
  config.vm.network "forwarded_port", guest: 22, host: VM_PORT
  config.vm.network "forwarded_port", guest: 80, host: VM_PORT2

  # Sync folder
  #config.vm.synced_folder HOST_PATH, GUEST_PATH

  # Disable default Vagrant folder, use a unique path per project
  #config.vm.synced_folder '.', '/home/'+VM_USER+'', disabled: true

  # Install Git, Node.js 6.x.x, Latest npm
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install python python-pycurl python-apt
    apt-get update
    apt-get upgrade -y
    apt-get autoremove -y
  SHELL

  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    ansible.playbook = "/etc/ansible/skeleton/vagrant.yml"
  end
end
