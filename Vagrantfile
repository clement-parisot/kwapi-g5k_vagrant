# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  config.vm.box = "debian/wheezy64"
  config.vm.synced_folder ".", "/tmp/kwapi-g5k", type: "rsync", rsync__args: ["--verbose", "--archive", "--delete", "-z"]

  config.vm.provision "shell", inline: <<-SHELL
    #!/bin/bash -x
    apt-get update
    apt-get -y --no-install-recommends install python-pip git debhelper python-all
    pip install stdeb
    # install dependencies
    cd /tmp/kwapi-g5k
    git clone https://github.com/lpouillo/kwapi-g5k.git
    cd kwapi-g5k
    git checkout network-monitoring-dev
    python setup.py --command-packages=stdeb.command bdist_deb
  SHELL

end
