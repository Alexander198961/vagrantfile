# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

  config.vm.define "dashboard" do  |dashboard| 
  dashboard.vm.box = "bento/ubuntu-16.04"


  dashboard.vm.network "private_network", ip: "192.168.50.5"
  dashboard.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update

    echo "192.168.50.6    openam.example.com" | sudo tee -a /etc/hosts
    sudo cp -r /vagrant/glassfish4 /opt/
    export JAVA_HOME=/vagrant/jdk1.8.0_121
    export PATH=$PATH:$JAVA_HOME/bin
    export GLASSFISH_HOME=/opt/glassfish4
    export PATH=$PATH:$GLASSFISH_HOME/bin
    echo "export JAVA_HOME=/vagrant/jdk1.8.0_121" | sudo tee -a /root/.bashrc 
    sudo echo "export PATH=$PATH:$JAVA_HOME/bin"  | sudo tee -a /root/.bashrc   
    echo "export GLASSFISH_HOME=/opt/glassfish4" | sudo tee -a /root/.bashrc
    sudo echo "export PATH=$PATH:$GLASSFISH_HOME/bin"  | sudo tee -a /root/.bashrc   
   sudo cp /vagrant/domain.xml /opt/glassfish4/glassfish/config
   sudo su 
   asadmin start-domain
   cd /vagrant
  SHELL
end

 config.vm.define "openam" do  |openam| 
  openam.vm.box = "bento/ubuntu-16.04"



 

   openam.vm.network "private_network", ip: "192.168.50.6"


   openam.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update

    echo "127.0.0.1   openam.example.com" | sudo tee -a /etc/hosts
    export JAVA_HOME=/vagrant/jdk1.8.0_121
    export PATH=$PATH:$JAVA_HOME/bin
    echo "export JAVA_HOME=/vagrant/jdk1.8.0_121" | sudo tee -a /root/.bashrc 
    sudo echo "export PATH=$PATH:$JAVA_HOME/bin"  | sudo tee -a /root/.bashrc   
    sudo su
    sudo apt-get -y install tomcat7
    sudo apt-get -y install unzip 
    mkdir /var/lib/tomcat7/webapps/openam
    cp /vagrant/openam.war /var/lib/tomcat7/webapps/openam


    sudo chown -R tomcat7:tomcat7 /var/lib/tomcat7/webapps/openam/
    sudo chown -R tomcat7:tomcat7 /usr/share/tomcat7
    sudo chmod g+w -R /var/lib/tomcat7/webapps/openam
    unzip /var/lib/tomcat7/webapps/openam/openam.war -d /var/lib/tomcat7/webapps/openam/

    sudo chown -R tomcat7:tomcat7 /usr/share/tomcat7
   cd /vagrant
   sudo cp /vagrant/server.xml /etc/tomcat7
   sudo cp /vagrant/tomcat7  /etc/default/
   sudo /etc/init.d/tomcat7 restart
  SHELL
end



 config.vm.define "nodejs"  do |node1|
  node1.vm.box = "bento/ubuntu-16.04"

  node1.vm.network "private_network", ip: "192.168.50.4"
  node1.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update

    echo "192.168.50.6    openam.example.com" | sudo tee -a /etc/hosts
    sudo apt-get -y install nodejs
    sudo nodejs /vagrant/main.js
  SHELL
end

config.vm.define "apache"  do |apache|
  apache.vm.box = "bento/ubuntu-16.04"


  apache.vm.network "forwarded_port", guest: 80, host: 80
  #apache.vm.network "public_network" 
  apache.vm.network "private_network", ip: "192.168.50.1"
  apache.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update

    echo "192.168.50.6    openam.example.com" | sudo tee -a /etc/hosts
    sudo apt-get -y install apache2   
    a2enmod rewrite
    sudo cp /vagrant/apache2.conf /etc/apache2
    sudo service apache2 restart    
  SHELL
end








config.vm.define "glvsmysql1"  do |glvsmysql1|
  glvsmysql1.vm.box = "bento/ubuntu-16.04"


  glvsmysql1.vm.network "private_network", ip: "192.168.50.10"  
  glvsmysql1.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update

    echo "192.168.50.6    openam.example.com" | sudo tee -a /etc/hosts
    export JAVA_HOME=/vagrant/jdk1.8.0_121


    sudo cp -r /vagrant/glassfish4 /opt/
    export PATH=$PATH:$JAVA_HOME/bin
    export GLASSFISH_HOME=/opt/glassfish4
    export PATH=$PATH:$GLASSFISH_HOME/bin
    echo "export JAVA_HOME=/vagrant/jdk1.8.0_121" | sudo tee -a /root/.bashrc
    sudo echo "export PATH=$PATH:$JAVA_HOME/bin"  | sudo tee -a /root/.bashrc
    echo "export GLASSFISH_HOME=/opt/glassfish4" | sudo tee -a /root/.bashrc
    sudo echo "export PATH=$PATH:$GLASSFISH_HOME/bin"  | sudo tee -a /root/.bashrc
   sudo su
   asadmin start-domain
   cd /vagrant
   sudo apt-get -y install debconf-utils
   sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password password root'
   sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root'
   sudo apt-get -y install mysql-server
  SHELL
end


config.vm.define "glvsmysql2"  do |glvsmysql2|
  glvsmysql2.vm.box = "bento/ubuntu-16.04"
  

  glvsmysql2.vm.network "private_network", ip: "192.168.50.11"  
  glvsmysql2.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update

    echo "192.168.50.6    openam.example.com" | sudo tee -a /etc/hosts
    export JAVA_HOME=/vagrant/jdk1.8.0_121
    export PATH=$PATH:$JAVA_HOME/bin


    sudo cp -r /vagrant/glassfish4 /opt/
    export GLASSFISH_HOME=/opt/glassfish4
    export PATH=$PATH:$GLASSFISH_HOME/bin
    echo "export JAVA_HOME=/vagrant/jdk1.8.0_121" | sudo tee -a /root/.bashrc
    sudo echo "export PATH=$PATH:$JAVA_HOME/bin"  | sudo tee -a /root/.bashrc
    echo "export GLASSFISH_HOME=/opt/glassfish4" | sudo tee -a /root/.bashrc
    sudo echo "export PATH=$PATH:$GLASSFISH_HOME/bin"  | sudo tee -a /root/.bashrc
   sudo su
   asadmin start-domain
   cd /vagrant
   sudo apt-get -y install debconf-utils
   sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password password root'
   sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root'
   sudo apt-get -y install mysql-server
  SHELL
end

config.vm.define "glvsmysql3"  do |glvsmysql3|
  glvsmysql3.vm.box = "bento/ubuntu-16.04"
 glvsmysql3.vm.network "private_network", ip: "192.168.50.12"  
 glvsmysql3.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    export JAVA_HOME=/vagrant/jdk1.8.0_121

    echo "192.168.50.6    openam.example.com" | sudo tee -a /etc/hosts
    sudo cp -r /vagrant/glassfish4 /opt/
    export PATH=$PATH:$JAVA_HOME/bin
    export GLASSFISH_HOME=/opt/glassfish4
    export PATH=$PATH:$GLASSFISH_HOME/bin
    echo "export JAVA_HOME=/vagrant/jdk1.8.0_121" | sudo tee -a /root/.bashrc
    sudo echo "export PATH=$PATH:$JAVA_HOME/bin"  | sudo tee -a /root/.bashrc
    echo "export GLASSFISH_HOME=/opt/glassfish4" | sudo tee -a /root/.bashrc
    sudo echo "export PATH=$PATH:$GLASSFISH_HOME/bin"  | sudo tee -a /root/.bashrc
   sudo su
   asadmin start-domain
   cd /vagrant
   sudo apt-get -y install debconf-utils
   sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password password root'
   sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root'
   sudo apt-get -y install mysql-server
  SHELL
end




end
