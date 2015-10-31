# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/trusty32"


  # For ipython notebook
  config.vm.network "forwarded_port", guest: 8888, host: 8888


  # config.vm.synced_folder "../data", "/vagrant_data"

  config.ssh.forward_agent = true
  config.ssh.forward_x11 = true

  config.vm.provider "virtualbox" do |vb|
    #   vb.gui = true
    vb.memory = "1024"
  end

  config.vm.provision "shell", inline: <<-SHELL
     sudo apt-get update
     sudo apt-get install -y lib64ncurses5-dev
     sudo apt-get install -y python3-pip
     sudo pip3 install --upgrade ipython[all]
     sudo pip3 install --upgrade jupyter
     sudo mkdir /vagrant/notebook
  SHELL

  config.vm.provision "shell", run: "always", inline: <<-SHELL
    ipython notebook --notebook-dir=/vagrant/notebook --no-browser --ip=0.0.0.0 &
  SHELL
end
