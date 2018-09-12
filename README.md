# Vagrant-test

*well this project is based on the vagrant and virtual box for installing the nginx server 
1) so firstly we download the vagrant and virtual box
2) after that we need to install vagrant ubuntu box for accesing the vagrant
3) so make the new folder and name it anything you want 
4) After that go to terminal and go to that dir that you were recently created 
5) and type comand vagrant init  ( So by doing this the vagrant file will generate and you have to paste some code in the vagrant file)

6) ######### Vagrant configuration ################################### 

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network :forwarded_port, guest: 80, host: 8080, auto_correct:true   # Nginx HTTP
  config.vm.network :forwarded_port, guest: 443, host: 8443, auto_correct:true   # Nginx HTTPS

 config.vm.provision "shell" do |s|
  s.path ="provision.sh"

end
end



7) after that write some bash script which you can install the packages in vagrant machine

8 ) by simply using that bash script
################################################

#!/bin/bash

echo "the virtual machine is starting..........."

echo "Installing Nginx......... Make check that you have a root user."

echo " type your root password"

sudo apt-get install nginx -y   #installing the nginix 

service nginx start

wget https://dl.eff.org/certbot-auto     #apply certbot ssl
chmod a+x certbot-auto
 sudo ./certbot-auto --nginx

sudo ./certbot-auto --nginx certonly

./certbot-auto renew   #this will auto renew the ssl

0 0,12 * * * python -c 'import random; import time; time.sleep(random.random() * 3600)' && ./certbot-auto renew


9 ) using this bash script you can easily install all the nginx server and https redirected ................

10 ) than go to terminal and type vagrant up --provision
it will perform all the operation whatever written in the bashscript.....


