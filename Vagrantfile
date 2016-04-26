VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.network "forwarded_port", guest: 5432, host: 5432
  config.vm.network "forwarded_port", guest: 8000, host: 8080
  config.vm.network "forwarded_port", guest: 8888, host: 8888

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 2048
    vb.cpus = 2
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo cp /vagrant/etc/bash.bashrc /etc/bash.bashrc
    sudo cp /vagrant/etc/vim/vimrc.local /etc/vim/vimrc.local
    sudo cp /vagrant/etc/postgresql/9.3/main/postgresql.conf /etc/postgresql/9.3/main/postgresql.conf
    sudo cp /vagrant/etc/postgresql/9.3/main/pg_hba.conf /etc/postgresql/9.3/main/pg_hba.conf
    sudo locale-gen en_US.UTF-8
    sudo dpkg-reconfigure locales
    sudo apt-get update
    sudo apt-get install python3-dev -y
    sudo apt-get install python3-setuptools -y
    sudo apt-get install libfreetype6 -y
    sudo apt-get install tk -y
    sudo apt-get install libpng12-dev -y
    sudo apt-get install libxft-dev -y
    sudo apt-get install g++ -y
    sudo apt-get install postgresql -y
    sudo apt-get install postgresql-contrib
    sudo pg_createcluster 9.3 main --start
    sudo service postgresql restart
    sudo -u postgres createuser -s vagrant
    sudo -u vagrant createdb
    sudo easy_install3 pip
    sudo pip3 install ipython
    sudo pip3 install numpy
    sudo pip3 install pandas
    sudo pip3 install matplotlib
    sudo pip3 install notebook
    sudo -su vagrant screen -dmS python-notebook bash -c "jupyter notebook --no-browser --ip=0.0.0.0 --port=8888 --port-retries=0" && echo "Jupyter Notebook has been started"
  SHELL

  # use graphical programs
  config.ssh.forward_x11 = true  
end
