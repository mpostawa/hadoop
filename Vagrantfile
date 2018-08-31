# -*- mode: ruby -*-
# vi: set ft=ruby :

#http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/ClusterSetup.html

PRIVATE_KEY_SOURCE      = 'id_rsa'
PUBLIC_KEY              = 'id'
PRIVATE_KEY_DESTINATION = '/home/vagrant/.ssh/id_rsa'
PUBLIC_KEY_DESTINATION  = '/home/vagrant/.ssh/authorized_keys'
MASTER_IP               = '192.168.51.4'
DATA1_IP                = '192.168.51.5'
DATA2_IP                = '192.168.51.6'

Vagrant.configure("2") do |config|

  config.ssh.insert_key = false

  # define Master server
  config.vm.define "master" do |master|
    master.vm.hostname = "hadoop-master"
    master.vm.box = "ubuntu/trusty64"
    master.vm.synced_folder ".", "/home/vagrant/src", mount_options: ["dmode=775,fmode=664"]
    master.vm.network "private_network", ip: MASTER_IP
    master.vm.provider "virtualbox" do |v|
      v.name = "master"
      v.cpus = 2
      v.memory = 2048
      #v.gui = true
    end
    # copy private key so hosts can ssh using key authentication (the script below sets permissions to 600)
    master.vm.provision :file do |file|
      file.source      = PRIVATE_KEY_SOURCE
      file.destination = PRIVATE_KEY_DESTINATION
    end
    master.vm.provision :file do |auth|
      auth.source      = PUBLIC_KEY
      auth.destination = PUBLIC_KEY_DESTINATION
    end
    master.vm.provision "shell", path: "bootstrap-master.sh"
  end

  # define data1 server
  config.vm.define "data1" do |data1|
    data1.vm.hostname = "hadoop-data1"
    data1.vm.box = "ubuntu/trusty64"
    data1.vm.network "private_network", ip: DATA1_IP
    data1.vm.provider "virtualbox" do |v|
      v.name = "data1"
      v.cpus = 2
      v.memory = 2048
    end
    # copy private key so hosts can ssh using key authentication (the script below sets permissions to 600)
    data1.vm.provision :file do |file|
      file.source      = PRIVATE_KEY_SOURCE
      file.destination = PRIVATE_KEY_DESTINATION
    end
    data1.vm.provision :file do |auth|
      auth.source      = PUBLIC_KEY
      auth.destination = PUBLIC_KEY_DESTINATION
    end

  end

  # define data2 server
  config.vm.define "data2" do |data2|
    data2.vm.hostname = "hadoop-data2"
    data2.vm.box = "ubuntu/trusty64"
    data2.vm.network "private_network", ip: DATA2_IP
    data2.vm.provider "virtualbox" do |v|
      v.name = "data2"
      v.cpus = 2
      v.memory = 2048
    end
    # copy private key so hosts can ssh using key authentication (the script below sets permissions to 600)
    data2.vm.provision :file do |file|
      file.source      = PRIVATE_KEY_SOURCE
      file.destination = PRIVATE_KEY_DESTINATION
    end
    data2.vm.provision :file do |auth|
      auth.source      = PUBLIC_KEY
      auth.destination = PUBLIC_KEY_DESTINATION
    end
  end

end
