# -*- mode: ruby -*-
# vi: set ft=ruby :

# The MIT License (MIT)
# 
# Copyright (c) 2016 Kevin Brightwell
#
# Permission is hereby granted, free of charge, to any person obtaining a copy 
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights 
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in
# all copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.

# This vagrantfile is used for building the procsim project through Jenkins. 
# Boxes should be created and installed from the subdirectories. 

Vagrant.configure("2") do |config|

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 1536
    vb.cpus = 2
    
    vb.gui = false
  end
  
  # Define the four platforms
  
  config.vm.define "trusty", autostart: false do |trusty|
    trusty.vm.box = "procsim/trusty"
  end

  config.vm.define "wily", autostart: false do |wily|
    wily.vm.box = "procsim/wily"
  end
 
  config.vm.define "osx", autostart: false do |osx|
    osx.vm.box = "procsim/osx"
    
    # We have to disable it here, it gets reset when this file is run unfortunately. 
    osx.vm.synced_folder ".", "/vagrant", disabled: true
    if ENV.has_key?("WORKSPACE")
        osx.vm.provision "shell", run: "always", inline: "echo 'Linking workspace: ~vagrant/workspace -> #{ENV["WORKSPACE"]}'"

        osx.vm.network "private_network", ip: "10.10.10.10"
        osx.vm.synced_folder ENV["WORKSPACE"], "/Users/vagrant/workspace",
            id: "workspace-root",
            :nfs => true,
            :mount_options => ['nolock','vers=3','tcp','noatime','actimeo=1','resvport']
    end
  end

  config.vm.define "win64", autostart: false do |trusty|
    trusty.vm.box = "procsim/win64"
  end

end

