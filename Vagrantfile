# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/xenial64"

  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
  end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    git clone https://github.com/batfish/batfish.git
    apt-get update -y
    apt-get upgrade -y
    apt-get install gcc g++ make automake autoconf libtool -y
    add-apt-repository ppa:fkrull/deadsnakes
    apt-get update -y
    apt-get install python2.7 python-pip -y
    apt-get install default-jdk ant -y
    cd batfish/
    sudo tools/install_z3_rhel_x86_64.sh /usr
    echo "source tools/batfish_functions.sh" >> ~/.bashrc
    source tools/batfish_functions.sh
    export ANT_OPTS=-Xmx1g
    batfish_build_all
    chown -R ubuntu:ubuntu /home/ubuntu/batfish/
    #allinone -cmdfile tests/basic/commands
    #allinone -runclient false
  SHELL
end
