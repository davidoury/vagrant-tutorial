# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  # Create machines running CentOS 7.1
  config.vm.box = "bento/centos-7.1" 

  # Run by all machines created below
  config.vm.provision "shell", inline: <<-PROV_ALL
    echo PROV_ALL
    echo hello | sudo passwd --stdin root
PROV_ALL

  # Configuration for box0
  config.vm.define "box0" do |box0|
    box0.vm.network "private_network", ip: "10.0.0.100"
    box0.vm.hostname = "box0"
		config.vm.provider "virtualbox" do |v|
  		v.memory = 512
  		v.cpus = 2
		end
    box0.vm.provision "shell", inline: <<-PROV_BOX0
    	echo PROV_BOX0
      echo "Hostname: " `hostname`
      touch /tmp/box0.hello.world
PROV_BOX0
  end

  # Configuration for box1
  config.vm.define "box1" do |box1|
    box1.vm.network "private_network", ip: "10.0.0.101"
    box1.vm.hostname = "box1"
		config.vm.provider "virtualbox" do |v|
  		v.memory = 1024
  		v.cpus = 1
		end
    box1.vm.network "forwarded_port", guest: 8080,  host: 18080
    box1.vm.network "forwarded_port", guest: 5050,  host: 15050
    box1.vm.provision "shell", inline: <<-PROV_BOX1
      echo PROV_BOX1
      echo "Hostname: " `hostname`
      touch /tmp/box1.hello.world
PROV_BOX1
  end

  # Configuration for box2
 config.vm.define "box2" do |box2|
   box2.vm.network "private_network", ip: "10.0.0.102"
   box2.vm.hostname = "box2"
    config.vm.provider :box do |vb|
      vb.customize ["modifyvm", :id, "--memory", "1500"]
    end
    box2.vm.network "forwarded_port", guest: 8080,  host: 28080
    box2.vm.network "forwarded_port", guest: 5050,  host: 25050
    box1.vm.provision "shell", inline: <<-PROV_BOX2
      echo PROV_BOX@
      echo "Hostname: " `hostname`
      touch /tmp/box2.hello.world
PROV_BOX2
 end

end

