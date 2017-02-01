# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

    config.vm.box = "rbayliss/PHP55"
    config.vm.network "private_network", type: "dhcp"
    config.vm.hostname = "rbayliss"
    config.vm.provider "virtualbox" do |v|
	  v.memory = 2048
	  v.cpus = 2
	end
    #config.vm.synced_folder "www", "/var/www", :nfs => { :mount_options => ["dmode=775", "fmode=664"] }
    #config.vm.synced_folder ".", "/vagrant", :nfs => { :mount_options => ["dmode=775", "fmode=664"] }
    config.vm.synced_folder "www", "/var/www", owner: "www-data", group: "vagrant", mount_options: ["dmode=775,fmode=664"]
    config.vm.synced_folder ".", "/home/vagrant/host", owner: "vagrant", group: "vagrant", mount_options: ["dmode=775,fmode=664"]
    config.vm.provision "shell", privileged: true, inline: <<-SHELL
cat /home/vagrant/.profile >> /home/vagrant/.bash_profile    
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 7638D0442B90D010 && \
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 9D6D8F6BC857C906 && \
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 7F438280EF8D349F && \ 
apt-get -y install vim && \
mkdir --parents /home/vagrant/bin && \
cd /tmp && \
wget https://files.magerun.net/n98-magerun.phar && \
chmod +x /tmp/n98-magerun.phar && \
chown -R vagrant: /home/vagrant/bin && \
mv /tmp/n98-magerun.phar /home/vagrant/bin/n98-magerun && \
cp /home/vagrant/host/conf.d/*.conf /etc/apache2/sites-available && \
for conf in /home/vagrant/host/conf.d/*.conf; do sudo a2ensite $(basename $conf); done && \
apachectl restart
    SHELL
end
