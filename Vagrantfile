# -*- mode: ruby -*-
# vi: set ft=ruby :

$GNOME = <<SCRIPT
sudo echo "GNOME###########################################################################"
sudo yum -y groupinstall "GNOME Desktop"
sudo systemctl set-default graphical.target
sudo systemctl start graphical.target
SCRIPT

$UPDATE = <<SCRIPT
sudo echo "UPDATE##########################################################################"
sudo yum -y update
SCRIPT

$GUEST = <<SCRIPT
sudo echo "GUEST###########################################################################"
sudo yum -y install epel-release gcc make perl kernel-devel kernel-headers wget
sudo wget http://download.virtualbox.org/virtualbox/5.2.8/VBoxGuestAdditions_5.2.8.iso
sudo mkdir /media/VBoxGuestAdditions
sudo mount -o loop,ro VBoxGuestAdditions_5.2.8.iso /media/VBoxGuestAdditions
sudo sh /media/VBoxGuestAdditions/VBoxLinuxAdditions.run
sudo rm VBoxGuestAdditions_5.2.8.iso
sudo umount /media/VBoxGuestAdditions
sudo rmdir /media/VBoxGuestAdditions
SCRIPT

$GOOGLE = <<SCRIPT
sudo wget https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm
sudo yum -y install ./google-chrome-stable_current_*.rpm
sudo rm -f ./google-chrome-stable_current_*.rpm
SCRIPT

Vagrant.configure("2") do |config|  
	
	config.vm.box = "centos/7"
	config.vm.hostname = "Base"	

	config.vm.provider "virtualbox" do |v|
		v.gui = true
		v.name = "Base"
		v.customize ["modifyvm", :id, "--cpus", "4"]
		v.customize ["modifyvm", :id, "--memory", "4096"]
		v.customize ["modifyvm", :id, "--vram", "128"]	
		v.customize ["modifyvm", :id, "--graphicscontroller", "vboxvga"]
		v.customize ["modifyvm", :id, "--ioapic", "on"]
		v.customize ["modifyvm", :id, "--hwvirtex", "on"]
		v.customize ["modifyvm", :id, "--accelerate3d", "on"]	
	end

	config.vm.provision "shell", inline: $UPDATE
	config.vm.provision :reload
	config.vm.provision "shell", inline: $GNOME
	config.vm.provision "shell", inline: $GUEST
	config.vm.provision "shell", inline: $UPDATE
	config.vm.provision :reload
	config.vm.provision "shell", inline: $GOOGLE
	
end
