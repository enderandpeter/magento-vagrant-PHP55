# magento-vagrant-PHP55
This is a Vagrantfile setup for deploying the [ubuntu/trusty64](https://atlas.hashicorp.com/ubuntu/boxes/trusty64/) Vagrantbox. It is good for web frameworks like [Magento 1](https://magento.com/tech-resources/download) that require PHP 5.5.

# Setup
Copy any conf files to be enabled on the VM into the `conf.d` folder. Next, run `vagrant up --provision` to make sure the provisioning inline-shell code is run that enables the httpd conf, provides the [n98-magerun](https://github.com/netz98/n98-magerun) command, and other important setup.

