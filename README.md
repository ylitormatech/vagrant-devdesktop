# CREATE DEVELOPER DESKTOP

## What will be installed into developer desktop

- Vagrant box ubuntu/trusty64 (Ubuntu 14.04)
- Virtualbox guest additions 5.0.24
- Ubuntu language files
- Gnome desktop
- NodeJS 6.3.x
- Gulp
- Bower
- Git
- Java 8 SDK
- Maven
- MongoDB
- CouchDB
- MySQL
- IntelliJ IDEA Ultimate 2016.2



# Pre-requirements

You need following installed beforehand:
- Vagrant
- VirtualBox 5.0.24+
- Cygwin (Windows Host)

# Installation



## Clone repository and move to project folder
- git clone https://github.com/ylitormatech/vagrant-devdesktop.git
- cd vagrant-devdesktop

## Create Virtual Machine (VM)

#### Update Vagrantfile
Note! Update Vagrantfile before creating VM

Change following lines depending how much resources of your host machine you want to give to VM:
- vb.memory = "4096"
- vb.cpus = 2
- vb.customize ["modifyvm", :id, "--vram", "96"]

#### Launch VM

- vagrant up

This might take 20-40 minutes.

#### set password for ubuntu user
- vagrant ssh devbox
If you are using windows, you should use e.g. cygwin terminal

When connection open:
- sudo passwd ubuntu
- exit

#### Shutdown VM
- vagrant halt

#### Start VM
- vagrant up

#### If you want to destroy VM
- vagrant destroy

