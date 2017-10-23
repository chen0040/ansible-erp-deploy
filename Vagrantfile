# -*- mode: ruby -*# vi: set ft=ruby :
require 'yaml'
vagrantConfig = YAML.load_file 'Vagrantfile.config.yml'
Vagrant.configure("2") do |config|
    config.vm.box = "bento/centos-7.4"

    config.vm.define "redis" do |redis|
        redis.vm.network "private_network", ip: vagrantConfig['ip']
        redis.vm.hostname = "redis"
    end

    config.vm.synced_folder "devops/", "/home/vagrant/devops", owner:"vagrant", group: "vagrant"

    # VirtualBox specific settings
    config.vm.provider "virtualbox" do |vb|
		vb.gui = false
		vb.memory = "4096"
		vb.cpus = 2
    end

    config.vm.provision "shell", inline: "sudo yum update -y"
    config.vm.provision "shell", inline: "sudo yum upgrade -y"
	config.vm.provision "shell", inline: "sudo yum groupinstall \"Development tools\" -y"
	
	# Install java and ansible
	config.vm.provision "shell", inline: "sudo yum install -y epel-release"
	config.vm.provision "shell", inline: "sudo yum install -y ansible"
	
	# Install build tools to build ruby
	# config.vm.provision "shell", inline: "sudo yum install gcc-c++ patch readline readline-devel zlib zlib-devel -y"
	# config.vm.provision "shell", inline: "sudo yum install libyaml-devel libffi-devel openssl-devel make -y"
	# config.vm.provision "shell", inline: "sudo yum install bzip2 autoconf automake libtool bison iconv-devel sqlite-devel dos2unix -y"
		
end
