# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|

	config.vm.define "devbox" do |devbox|
	  devbox.vm.box = "ubuntu/trusty64"
	  
	  devbox.vm.network "forwarded_port", guest: 80, host: 8787
	  
	  
	  # Create a private network, which allows host-only access to the machine
	  # using a specific IP.
	  devbox.vm.network "private_network", ip: "192.168.33.11"

	  # Create a public network, which generally matched to bridged network.
	  # Bridged networks make the machine appear as another physical device on
	  # your network.
	  # devbox.vm.network "public_network"

	  # Share an additional folder to the guest VM. The first argument is
	  # the path on the host to the actual folder. The second argument is
	  # the path on the guest to mount the folder. And the optional third
	  # argument is a set of non-required options.
	  devbox.vm.synced_folder "D:/projects/vagrant/devbox1.1/shared", "/vagrant_data"

	  devbox.vm.provider "virtualbox" do |vb|
		# Display the VirtualBox GUI when booting the machine
		vb.gui = true
		vb.name = "devbox1.2"
		# Customize the amount of memory on the VM:
		vb.memory = "1500"
		vb.cpus = 2
		vb.customize ["modifyvm", :id, "--vram", "96"]
	  end


	  # Enable provisioning with a shell script. Additional provisioners such as
	  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
	  # documentation for more information about their specific syntax and use.
	  devbox.vm.provision "shell", inline: <<-SHELL
		sudo apt-get update
		# Install GUI: gnome
		#sudo apt-get install gnome-terminal -y
		sudo apt-get install dictionaries-common -y
		sudo apt-get install aspell -y
		sudo apt-get install myspell-dictionary -y
		sudo apt-get install libwebkitgtk-3.0-0 -y
		sudo apt-get install zenity -y
		sudo apt-get install gedit -y
		sudo apt-get install gnome-control-center -y
		sudo apt-get install gnome-documents -y
		sudo apt-get install gnome-online-accounts -y
		sudo apt-get install gnome-sushi -y
		sudo apt-get install mutter -y
		sudo apt-get install ubuntu-release-upgrader-gtk -y
		sudo apt-get install yelp -y
		
		sudo apt-get install ubuntu-gnome-desktop -y

		
		
		# Install language support
		sudo apt-get install -y language-selector-gnome
		sudo apt-get -y install language-pack-fi
		sudo apt-get -y install language-pack-en
		#copy new locale from shared folder
		# next line does not work. language setting must be doen manually from gui
		# yes | sudo cp -rf /vagrant/shared/locale /etc/default
		sudo apt-get update
		
		# Install virtualbox guest additions
		cd /opt
		sudo wget -c http://download.virtualbox.org/virtualbox/5.0.24/VBoxGuestAdditions_5.0.24.iso -O VBoxGuestAdditions_5.0.24.iso
		sudo mount VBoxGuestAdditions_5.0.24.iso -o loop /mnt
		cd /mnt
		yes | sudo sh VBoxLinuxAdditions.run --nox11 
		cd /opt
		sudo rm *.iso
		sudo /etc/init.d/vboxadd setup
		
		sudo apt-get install sysv-rc-conf -y
		sudo sysv-rc-conf vboxadd on
		sudo apt-get update
		
		
		
		
		# Install NODEJS 6.3
		curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
		sudo apt-get install -y nodejs
		sudo apt-get update
		
		
		# Install javascript tools
		npm install -g -y gulp bower
		
		
		# Install GIT
		sudo apt-get install -y git 
		
		
		# Install JAVA 8 SDK
		echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections
		sudo add-apt-repository -y ppa:webupd8team/java
		sudo apt-get update
		sudo apt-get install -y oracle-java8-installer
		
		# Install MAVEN
		sudo apt-get install -y maven
		
		# Install MONGODB
		sudo apt-get install mongodb -y
		
		 # Install COUCHDB
		sudo add-apt-repository ppa:couchdb/stable -y
		sudo apt-get update
		sudo apt-get install couchdb -y
		
		# Install MYSQL
		debconf-set-selections <<< "mysql-server mysql-server/root_password password vagrant"
		debconf-set-selections <<< "mysql-server mysql-server/root_password_again password vagrant"
		sudo apt-get install mysql-server -y
		mysql -uroot -pvagrant -e "CREATE DATABASE testidb"
		mysql -uroot -pvagrant -e "grant all privileges on testidb.* to 'testiuser'@'localhost' identified by 'password'"
		sudo apt-get update
		install sensing-world dev databases
		sensing-world-auth db
		mysql -uroot -pvagrant -e "CREATE DATABASE userserver"
		mysql -uroot -pvagrant -e "grant all privileges on userserver.* to 'userserver'@'localhost' identified by 'userserver'"
		sensing-world-base db
		mysql -uroot -pvagrant -e "CREATE DATABASE sensorserver"
		mysql -uroot -pvagrant -e "grant all privileges on sensorserver.* to 'sensorserver'@'localhost' identified by 'sensorserver'"

	   
		
		# Install Intellij Idea Ultimate
		cd /home/vagrant
		wget "https://download.jetbrains.com/idea/ideaIU-2016.2.tar.gz"
		mkdir /opt/ideaIU
		tar -xvzf ideaIU-2016.2.tar.gz -C /opt/ideaIU --strip-components=1
		chmod 755 /opt/ideaIU/bin/idea.sh
		yes | cp -rf /vagrant/shared/idea.desktop /usr/share/applications
		sudo chmod 644 /usr/share/applications/idea.desktop
		sudo chown root:root /usr/share/applications/idea.desktop
	  SHELL
	  end
end
