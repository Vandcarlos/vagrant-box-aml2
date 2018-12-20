#!/usr/bin/ruby

Vagrant.configure("2") do |config|
  config.vm.box = "vandcarlos/aml2"
  config.vm.box_version = "0.0.1"
  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
  end
  config.ssh.username = "ec2-user"
  config.vm.network "private_network", ip: "192.168.33.10"
  config.ssh.insert_key = false

  config.vm.define "base", autostart: false do |base|
    base.vm.box = "aml2"
    base.vm.box_version = ""

    base.vm.provision "ansible" do |ansible|
      ansible.playbook = "amazon-base-image/playbook.yml"
      ansible.groups = {
        "aml2" => ["base"]
      }
    end
  end

  config.vm.define "aml2", autostart: true, primary: true do |default|
    default.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
    end
  end
end
