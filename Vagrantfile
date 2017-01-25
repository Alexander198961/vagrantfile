# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
 
  config.vm.define "glassfish1" do  |gl1| 

  gl1.vm.box = "bento/ubuntu-16.04"
  gl1.vm.provision "shell", inline: <<-SHELL

     sudo apt-get update
    
    export JAVA_HOME=/vagrant/jdk1.8.0_121
    export PATH=$PATH:$JAVA_HOME/bin
    export GLASSFISH_HOME=/vagrant/glassfish4
    export PATH=$PATH:$GLASSFISH_HOME/bin
    echo "export JAVA_HOME=/vagrant/jdk1.8.0_121" | sudo tee -a /root/.bashrc 
    sudo echo "export PATH=$PATH:$JAVA_HOME/bin"  | sudo tee -a /root/.bashrc   
    echo "export GLASSFISH_HOME=/vagrant/glassfish4" | sudo tee -a /root/.bashrc
    sudo echo "export PATH=$PATH:$GLASSFISH_HOME/bin"  | sudo tee -a /root/.bashrc   
   cp /vagrant/domain.xml /vagrant/glassfish4/glassfish/config
   sudo su 
   asadmin start-domain
   cd /vagrant
   sudo apt-get -y install debconf-utils 
   sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password password root'
   sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root'
   sudo apt-get -y install mysql-server

  # sudo nodejs main.js for nodejs -server
  SHELL
end
 config.vm.define "nodejs"  do |node1|
 
  node1.vm.box = "bento/ubuntu-16.04"
  node1.vm.provision "shell", inline: <<-SHELL
  
    sudo apt-get update
  SHELL
end
end
