# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.hostname = "jenkins"
  config.vm.network "forwarded_port", guest:9000 , host: 8080
  config.vm.network "forwarded_port", guest:4200, host:80
  config.vm.network "forwarded_port", guest:8080 , host: 8080  
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.provision "shell", inline: <<-SHELL
    yum install epel-release -y
    yum install python-pip -y
    pip install ansible
  SHELL

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
  end

end
