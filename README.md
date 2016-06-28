# procsim-bld
Repository for build information for the procsim project.

This repository is used by the Master Jenkins node when building. 

## Common Configuration

When provisioning, all boxes accept an environment variable: `WORKSPACE` which 
is the directory linked into `~vagrant/workspace`. This is utilized by Jenkins
and can be utilized by develops as necessary. 

## Boxes

* wily
  Base Box: [`ubuntu/wily64`](https://atlas.hashicorp.com/ubuntu/boxes/wily64)
  
  Software:
    * `clang-3.7`
    * `gcc-5`
    * `cmake`
    * `ninja`
    * `qt5`

* trusty
  Base Box: [`ubuntu/trusty64`](https://atlas.hashicorp.com/ubuntu/boxes/trusty64)
  
  Software:
    * `clang-3.7`
    * `gcc-5`
    * `cmake`
    * `ninja`
    * `qt5`


* osx-fresh
  Base Box: [`jhcook/osx-elcapitan-10.11`](https://atlas.hashicorp.com/jhcook/boxes/osx-elcapitan-10.11)
  
  Software:
    * `cmake`
    * `ninja`
    * `qt5`
    * `xcode` CLI tools, no full installation
    * `brew`

  The Version used within Jenkins has Xcode installed in full. 

* osx-custom
  Base Box: [`AndrewDryga/vagrant-box-osx`](https://github.com/AndrewDryga/vagrant-box-osx). 
  The `Vagrantfile` is not complete as installing the full xcode installation
  is not available from the commandline. 
  
  Software:
    * `cmake`
    * `ninja`
    * `qt5`
    * `xcode` full installation
    * `brew`