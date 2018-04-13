# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.ssh.insert_key = false
  config.vm.synced_folder './data', '/vagrant', type: 'nfs'
  
  config.vm.define "kbmaster" do |kbmaster|
    kbmaster.vm.hostname = "kbmaster"
    kbmaster.vm.box = "bento/ubuntu-16.04"
    kbmaster.vm.network "forwarded_port", guest: 12345, host: 12345 
    kbmaster.vm.network :private_network, ip: "192.168.33.145"

    kbmaster.vm.provider :kbmaster do |v|
      v.gui = false
      v.memory = 256
      v.cpus = 1
      config.vm.synced_folder "./data", "/vagrant", disabled: true
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--ioapic", "on"]
    end

    kbmaster.vm.provision "shell", inline: "echo kbmaster Ready"
  end

  config.vm.define "kbslave1" do |kbslave1|
    kbslave1.vm.hostname = "kbslave1"
    kbslave1.vm.box = "bento/ubuntu-16.04"
    kbslave1.vm.network "forwarded_port", guest: 12346, host: 12346 
    kbslave1.vm.network :private_network, ip: "192.168.33.146"

    kbslave1.vm.provider :kbslave1 do |v|
      v.gui = false
      v.memory = 256
      v.cpus = 1
      config.vm.synced_folder "./data", "/vagrant", disabled: true
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--ioapic", "on"]
    end

    kbslave1.vm.provision "shell", inline: "echo kbslave1 Ready"
  end

  config.vm.define "kbslave2" do |kbslave2|
    kbslave2.vm.hostname = "kbslave2"
    kbslave2.vm.box = "bento/ubuntu-16.04"
    kbslave2.vm.network "forwarded_port", guest: 12347, host: 12347 
    kbslave2.vm.network :private_network, ip: "192.168.33.147"

    kbslave2.vm.provider :kbslave2 do |v|
      v.gui = false
      v.memory = 256
      v.cpus = 1
      config.vm.synced_folder "./data", "/vagrant", disabled: true
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--ioapic", "on"]
    end

    kbslave2.vm.provision "shell", inline: "echo kbslave2 Ready"
  end
  
  config.vm.define "ansible" do |ansible|
    ansible.vm.hostname = "ansible"
    ansible.vm.box = "bento/ubuntu-16.04"
    ansible.vm.network "forwarded_port", guest: 12348, host: 12348 
    ansible.vm.network :private_network, ip: "192.168.33.148"

    ansible.vm.provider :ansible do |v|
      v.gui = false
      v.memory = 256
      v.cpus = 1
      config.vm.synced_folder "./data", "/vagrant", disabled: true
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--ioapic", "on"]
    end
    ansible.vm.provision "file", source: "./playbooks", destination: "~/playbooks"
    ansible.vm.provision "shell", inline: "echo ansible Ready"
    ansible.vm.provision "shell", inline: "sudo apt-get update -y && sudo apt-get install -y ansible"
  end
   
end
