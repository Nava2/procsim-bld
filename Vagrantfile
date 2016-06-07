# -*- mode: ruby -*-
# vi: set ft=ruby :

# It is recommended to install the vbguest plugin:
# vagrant plugin install vagrant-vbguest

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

with_gui = ENV.has_key?("WITH_GUI") ? true : false

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 2048
    vb.cpus = 2
  end
  
  # Define the four platforms
  
  config.vm.define "trusty", autostart: false do |trusty|
    trusty.vm.box = "procsim/trusty"
    
    trusty.vm.provider "virtualbox" do |vb|
      vb.name = "hc12sim_trusty"
    end 
  end
 
  config.vm.define "osx", autostart: false do |osx|
    osx.vm.box = "procsim/osx"
    
    osx.vm.provider "virtualbox" do |vb|
      vb.name = "hc12sim_osx"
      vb.gui = false
    end 

    osx.vm.network "private_network", ip: "10.10.10.10"
    osx.vm.synced_folder ".", "/Users/vagrant/vagrant",
        id: "vagrant-root",
        :nfs => true,
        :mount_options => ['nolock,vers=3,tcp,noatime,actimeo=1,resvport']
 
  end

  config.vm.define "win64", autostart: false do |trusty|
    trusty.vm.box = "procsim/win64"
    
    trusty.vm.provider "virtualbox" do |vb|
      vb.name = "hc12sim_win64"
    end 
  end

  # Required to have the guest-utils work properly
  config.vm.provision :reload

end

