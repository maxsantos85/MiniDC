# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/bionic64"

  ##VM1
  config.vm.define "db" do |db|
    db.vm.hostname = "database"
    db.vm.network :private_network, ip: "172.17.177.21"
    db.vm.provider :virtualbox do |v|
      v.name = "MiniDC-Database"
      v.memory = 512
      v.cpus = 1
    end
  end

  ##VM2
  config.vm.define "web" do |web|
    web.vm.hostname = "blog"
    web.vm.network :private_network, ip: "172.17.177.22"
    web.vm.provider :virtualbox do |v|
      v.name = "MiniDC-Blog"
      v.memory = 512
      v.cpus = 1
    end
  end

  ##VM3
  config.vm.define "controller" do |controller|
    controller.vm.hostname = "controller"
    controller.vm.network :private_network, ip: "172.17.177.11"
    
    # Restringindo o permissionamento da pasta Vagrant
    controller.vm.synced_folder "./", "/vagrant", mount_options: ["dmode=750,fmode=600"]

    controller.vm.provider :virtualbox do |v|
      v.name = "MiniDC-AnsibleController"
      v.memory = 512
      v.cpus = 1
    end
    ## Integrando o Ansible no Provisionamento
    controller.vm.provision :ansible_local do |ansible|
      ansible.install_mode = "default"
      ansible.playbook = "playbook.yml"
      ansible.inventory_path = "inventory"
      ansible.verbose  = true
      ansible.install  = true
      ansible.limit    = "all"
    end
  end

end

