# -*- mode: ruby -*-
# vi: set ft=ruby :

BOX_IMAGE = "bento/ubuntu-22.04"
MEMORY = "2048"
CPU = "2"


Vagrant.configure("2") do |config|
  config.vm.define "node1" do |subconfig|
    subconfig.vm.box = BOX_IMAGE
    subconfig.vm.hostname = "node1"
	subconfig.vm.network :public_network, ip: "192.168.0.50"
	subconfig.vm.provider :virtualbox do |vb|
          vb.customize ["modifyvm", :id, "--memory", MEMORY]
          vb.customize ["modifyvm", :id, "--cpus", CPU]
	end
  end
  #Install some additional packages 
  config.vm.provision "shell", inline: <<-SHELL
	sudo su
	sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
    systemctl restart sshd.service
	apt-get install nano -y
	apt-get install net-tools -y
  SHELL
end