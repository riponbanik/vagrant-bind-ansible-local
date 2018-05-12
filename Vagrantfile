# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "centos/7"
  config.ssh.insert_key = false

 
  # set host dns
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]      
  end 

  config.vm.define "ns53" do |machine|
    machine.vm.hostname = "ns53.lab.local"
    machine.vm.network "private_network", ip: "192.168.56.16"        
  end


  # Enable Password Auth  
  config.vm.provision "auth", type: "shell", inline: <<-EOC
    sudo sed -i -e "\\#PasswordAuthentication no# s#PasswordAuthentication no#PasswordAuthentication yes#g" /etc/ssh/sshd_config
    sudo service sshd restart
  EOC

  # Shell
  config.vm.provision "shell", inline: <<-SHELL
    sudo yum -y install nano net-tools bind-utils       
  SHELL

  # Ansible
  config.vm.provision :ansible_local do |ansible|
    ansible.playbook       = "playbook.yml"
    ansible.verbose        = true
    ansible.install        = true
    ansible.install_mode = "pip"
    ansible.version = "2.4.3.0"
    ansible.become = true                
    ansible.limit          = "all" # or only "nodes" group, etc.
    ansible.inventory_path = "inventory"
  end 

end
