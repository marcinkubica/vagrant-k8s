# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define "control" do |control|
    control.vm.box="ubuntu/focal64"
    control.vm.network "private_network", ip: "10.0.0.9"
    control.vm.network "forwarded_port", guest: 22, host: 60200, protocol: "tcp"
    control.vm.network "forwarded_port", guest: 6443, host: 6443, protocol: "tcp"
    # Uncomment to get and IP from your DHCP - ie. at home
    # https://www.vagrantup.com/docs/networking/public_network
    #config.vm.network "public_network", bridge: "eno1"
    control.vm.hostname = "control"

    control.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "2048" ]
      vb.customize ["modifyvm", :id, "--cpus", "4" ]
      end
  end

  config.vm.define "node-01" do |node01|
    node01.vm.box="ubuntu/focal64"
    node01.vm.network "private_network", ip: "10.0.0.10"
    node01.vm.network "forwarded_port", guest: 22, host: 60201, protocol: "tcp"
    node01.vm.hostname = "node-01"

   node01.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "4096" ]
      vb.customize ["modifyvm", :id, "--cpus", "4" ]
      end
   end


  config.vm.define "node-02" do |node02|
    node02.vm.box="ubuntu/focal64"
    node02.vm.network "private_network", ip: "10.0.0.11"
    node02.vm.network "forwarded_port", guest: 22, host: 60202, protocol: "tcp"

    node02.vm.hostname = "node-02"

    node02.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "4096" ]
      vb.customize ["modifyvm", :id, "--cpus", "4" ]
      end
  end

  # Uncomment if you wish to execute at 'vagrant up'
  #
  #config.trigger.after :up do |trigger|
  #  trigger.name = "ansible trigger"
  #  trigger.info = "Attempting to run ansible-playbook site.yaml"
  #  trigger.run  = { path: "vagrant-k8s.sh" }
  #end

end



