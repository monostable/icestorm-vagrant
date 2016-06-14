# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2500" # this needs to be large for compilation
    vb.customize ['modifyvm', :id, '--usb', 'on']
    vb.customize ['usbfilter', 'add', '0', '--target', :id, '--name', 'Lattice FTUSB Interface Cable', '--vendorid', '0x0403', '--productid', '0x6010']
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y build-essential clang bison flex libreadline-dev gawk tcl-dev libffi-dev git mercurial graphviz xdot pkg-config python python3 libftdi-dev iverilog

    cd /tmp
    git clone https://github.com/cliffordwolf/icestorm.git icestorm
    cd /tmp/icestorm
    git checkout 49e3ad404a28faa1dbcbbc0acf3071bec3d5ddfe
    make -j2
    make install

    cd /tmp
    git clone https://github.com/cseed/arachne-pnr.git arachne-pnr
    cd /tmp/arachne-pnr
    git checkout 6b8336497800782f2f69572d40702b60423ec67f
    make -j2
    make install

    cd /tmp
    git clone https://github.com/cliffordwolf/yosys.git yosys
    cd yosys
    git checkout 99edf249669158b8c8bef0c7c3b926a2bbb7a621
    make -j2
    make install
   SHELL
end
