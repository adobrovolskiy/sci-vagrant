VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 2048
    vb.cpus = 2
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install python3-dev -y
    sudo apt-get install python3-setuptools -y
    sudo apt-get install libfreetype6 -y
    sudo apt-get install tk -y
    sudo apt-get install libpng12-dev -y
    sudo apt-get install libxft-dev -y
    sudo apt-get install g++ -y
    sudo easy_install3 pip
    sudo pip3 install ipython
    sudo pip3 install numpy
    sudo pip3 install pandas
    sudo pip3 install matplotlib
  SHELL

  # use graphical programs
  config.ssh.forward_x11 = true  
end
