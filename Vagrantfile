# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-20.04"

  config.vm.define :automation, primary: true do |automation|
    automation.vm.network "forwarded_port", host: 8180, guest: 8080
    automation.vm.network "private_network", ip: "10.0.1.10"
    automation.vm.hostname = "automation"
  end

  config.vm.define :production do |production|
    production.vm.network "private_network", ip: "10.0.1.11"
    production.vm.network "forwarded_port", host: 8280, guest: 80
    production.vm.hostname = "production"
  end
  
  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "provisioning/playbook.yml"
    ansible.groups = {
      "automationservers" => ["automation"],
      "webservers" => ["production"]
    }
  end

end
