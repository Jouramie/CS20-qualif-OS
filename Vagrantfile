Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get upgrade
    apt-get install -y make gcc g++ python cmake
  SHELL

  config.vm.provider "virtualbox" do |vbox|
    vbox.customize ["modifyvm", :id, "--uartmode1", "disconnected"] 
  end

  config.vm.provision "shell", inline: <<-SHELL
    cd /vagrant/os/private
    make
    sudo make install
    cp /vagrant/os/csgames.c /home/vagrant/
    cp /vagrant/os/poop.pdf /home/vagrant/
    cp /vagrant/os/readme.en.md /home/vagrant/
    cp /vagrant/os/readme.fr.md /home/vagrant/
    cp /vagrant/os/startup_simulator.py /home/vagrant/
  SHELL

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get clean
    sudo dd if=/dev/zero of=/EMPTY bs=1M
    sudo rm -f /EMPTY
    cat /dev/null > ~/.bash_history && history -c
  SHELL

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
