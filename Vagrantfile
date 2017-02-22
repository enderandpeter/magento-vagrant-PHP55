# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

    config.vm.box = "ubuntu/trusty64"
    config.vm.network "private_network", type: "dhcp"
    config.vm.hostname = "trusty64"
    config.vm.provider "virtualbox" do |v|
	  v.memory = 2048
	  v.cpus = 2
	  v.name = "magento"
	end
    #config.vm.synced_folder "www", "/var/www", :nfs => { :mount_options => ["dmode=775", "fmode=664"] }
    #config.vm.synced_folder ".", "/home/vagrant/host", :nfs => { :mount_options => ["dmode=775", "fmode=664"] }
    config.vm.synced_folder "www", "/var/www", owner: "www-data", group: "vagrant", mount_options: ["dmode=775,fmode=664"]
    config.vm.synced_folder ".", "/home/vagrant/host", owner: "vagrant", group: "vagrant", mount_options: ["dmode=775,fmode=664"]
    config.vm.provision "shell", privileged: true, inline: <<-SHELL
cat /home/vagrant/.profile >> /home/vagrant/.bash_profile    
apt-get -y update && \
sudo debconf-set-selections <<< 'mysql-server-5.6 mysql-server/root_password password root' && \
sudo debconf-set-selections <<< 'mysql-server-5.6 mysql-server/root_password_again password root' && \
apt-get -y install apache2 php5 php5-mcrypt php5-mysqlnd php5-curl php5-gd mysql-client-5.6 mysql-server-5.6 && \
php5enmod mcrypt && \
mkdir --parents /home/vagrant/bin && \
cd /tmp && \
wget https://files.magerun.net/n98-magerun.phar && \
chmod +x /tmp/n98-magerun.phar && \
chown -R vagrant: /home/vagrant/bin && \
mv /tmp/n98-magerun.phar /home/vagrant/bin/n98-magerun && \
cp /home/vagrant/host/conf.d/*.conf /etc/apache2/sites-available && \
for conf in /home/vagrant/host/conf.d/*.conf; do sudo a2ensite $(basename $conf); done && \
a2enmod rewrite && \
apachectl restart && \
echo " \n\
[mysqld] \n\
character-set-server = utf8 \n\
bind-address = 0.0.0.0 \n\
" >> /etc/mysql/conf.d/local.cnf && \
service mysql restart && \
if [ -e /home/vagrant/host/etc/provision.sh ]; then cp /home/vagrant/host/etc/provision.sh /home/vagrant/bin && chmod +x /home/vagrant/bin/provision.sh && /home/vagrant/bin/provision.sh; fi
    SHELL
end
