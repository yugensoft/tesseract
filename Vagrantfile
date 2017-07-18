# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-14.04"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
   config.vm.provider "virtualbox" do |vb|
     # Display the VirtualBox GUI when booting the machine
     # vb.gui = true

     # Customize the amount of memory on the VM:
     vb.memory = "2048"
   end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    # install dependencies
    echo Installing dependencies...
    apt-get update

    apt-get install -y g++ 
    apt-get install -y autoconf automake libtool
    apt-get install -y autoconf-archive
    apt-get install -y pkg-config
    apt-get install -y libpng12-dev
    apt-get install -y libjpeg8-dev
    apt-get install -y libtiff5-dev
    apt-get install -y zlib1g-dev
    apt-get install -y libicu-dev
    apt-get install -y libpango1.0-dev
    apt-get install -y libcairo2-dev

    apt-get install -y zip

    # install leptonica
    echo Installing leptonica...
    cd /home/vagrant
    wget -q https://github.com/DanBloomberg/leptonica/archive/1.74.4.zip
    unzip 1.74.4.zip
    cd leptonica*
    ./autobuild
    ./configure
    make 
    make install

    # install tesseract
    echo Installing tesseract
    cd /vagrant
    ./autogen.sh
    ./configure
    make
    make install
    make install-langs
    ldconfig
    # get language file for english
    echo Getting English language data...
    cd /usr/local/share/
    wget -q https://github.com/tesseract-ocr/tessdata/raw/4.00/eng.traineddata

    echo Finished.

  SHELL

end
