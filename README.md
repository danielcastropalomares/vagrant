# vagrant

This repository is destined to upload my vagrant configuration with ansible.

# First step

Requirements:
* Virtualbox
* Ubuntu/Debian

How install and use vagrant:

You can download the vagrant pacakge fromt te oficial web:
https://www.vagrantup.com/downloads.html
For Debian/ubuntu:
```
dpkg -i vagrant_2.1.2_x86_64.deb
```

Create folder vagrant on your home (or any location what you prefer):
```
mkdir ~/vagrant
```
And for every template create a new folder:
```
mkdir ~/vagrant/debian-vm
```
Now you can download the file Vagrantfile from this repository and put inside the directory Vagrantfile.

If you can't use any playbook for ansible, comment this lines:

```
  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    ansible.playbook = "/etc/ansible/skeleton/vagrant.yml"
  end
end
```
Execute the next command for initialize the machine and apply playbook (if you configured this):
```
cd /etc/ansible/skeleton/vagrant.yml
vagrant up --provision
```
After deploy, you can access to machine with
```
vagrant ssh
```
If you need reload config of vagrant:
```
vagrant reload --provision
```
