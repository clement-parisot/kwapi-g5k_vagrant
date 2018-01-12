# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  config.vm.box = "debian/wheezy64"
  config.vm.synced_folder ".", "/tmp/kwapi-g5k"

  config.vm.provision "shell", inline: <<-SHELL
    #!/bin/bash -x
    apt-get update
    apt-get -y --no-install-recommends install python-pip git debhelper python-all wget build-essential
    pip install stdeb
    # Copy version of kwapi (or clone repository)
    cp -R /tmp/kwapi-g5k/* .
    if [ ! -d kwapi-g5k ]
        then git clone https://github.com/grid5000/kwapi-g5k.git
    fi
    cd kwapi-g5k/
    git pull
    # Patch setup file and init script
    cp ../setup.py .
    cp ../kwapi etc/init/
    # Build packet
    rm -rf deb_dist/*
    export DISTUTILS_DEBUG="YES"; python setup.py --command-packages=stdeb.command bdist_deb
    # Export builded packet
    find . -name *.deb -type f -exec cp {} /tmp/kwapi-g5k/ \\;
  SHELL

end
