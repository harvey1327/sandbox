# -*- mode: ruby -*-
# vi: set ft=ruby :

$GNOME = <<SCRIPT
sudo yum -y groupinstall "GNOME Desktop"
sudo systemctl set-default graphical.target
sudo systemctl start graphical.target
SCRIPT

$GUEST = <<SCRIPT
sudo yum -y install linux-headers-$(uname -r) build-essential dkms
sudo wget http://download.virtualbox.org/virtualbox/5.2.8/VBoxGuestAdditions_5.2.8.iso
sudo mkdir /media/VBoxGuestAdditions
sudo mount -o loop,ro VBoxGuestAdditions_5.2.8.iso /media/VBoxGuestAdditions
sudo sh /media/VBoxGuestAdditions/VBoxLinuxAdditions.run
sudo rm VBoxGuestAdditions_5.2.8.iso
sudo umount /media/VBoxGuestAdditions
sudo rmdir /media/VBoxGuestAdditions
SCRIPT

Vagrant.configure("2") do |config|  
	
	config.vm.box = "centos/7"

	config.vm.provider "virtualbox" do |v|
		#v.gui = true
		v.customize ["modifyvm", :id, "--cpus", "2"]
		v.customize ["modifyvm", :id, "--memory", "4096"]
		v.customize ["modifyvm", :id, "--vram", "128"]	
	end

	#config.vm.provision "shell", inline: $GNOME
	config.vm.provision "shell", inline: $GUEST
	#config.vm.provision "shell", inline: "sudo yum -y upgrade"
	
end
