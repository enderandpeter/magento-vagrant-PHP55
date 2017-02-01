# magento-vagrant-PHP55
This is a Vagrantfile setup for deploying the [rbayliss/PHP55](https://atlas.hashicorp.com/rbayliss/boxes/PHP55) Vagrantbox. It is good for web applications like [Magento 1](https://magento.com/tech-resources/download) that require PHP 5.5.

# Setup
Copy any conf files to be enabled on the VM into the `conf.d` folder. Next, run `vagrant up --provision` to make sure the provisioning inline-shell code is run that enables the httpd conf, provides the [n98-magerun](https://github.com/netz98/n98-magerun) command, and other important setup.

## Features
Some common commands, like `ifconfig` and `apachectl` require `sudo` to run but won't need a password, which should still be `vagrant`.

You can run the `ww` command to enter a bash shell as the `www-data` user. 