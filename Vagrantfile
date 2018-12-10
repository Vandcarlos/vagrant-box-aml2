#!/usr/bin/ruby

Vagrant.configure("2") do |config|
  config.vm.box = "aml2"
  config.vm.provider "virtualbox"
  config.ssh.username = "ec2-user"
  config.vm.network "private_network", ip: "192.168.33.10"
end
