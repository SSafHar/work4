# Odeon

## Software

* VirtualBox - [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)
* Vagrant - [https://www.vagrantup.com/downloads.html](https://www.vagrantup.com/downloads.html)
* GIT - [https://git-scm.com/downloads](https://git-scm.com/downloads)

## Odeon links

Backend API: [http://api.192.168.33.208.xip.io](http://api.192.168.33.208.xip.io)

API documentation: [http://doc-api.192.168.33.208.xip.io](http://doc-api.192.168.33.208.xip.io)

Elastic search HQ: [http://eshq.192.168.33.208.xip.io](http://eshq.192.168.33.208.xip.io)

Elastic search rest: [http://192.168.33.208:9200](http://192.168.33.208:9200)

RockMongo: [http://rockmongo.192.168.33.208.xip.io/](http://rockmongo.192.168.33.208.xip.io/)


## Clean setup

Clone `odeon-vagrant` sources:

    git clone https://github.com/sorinbb/odeon-vagrant.git

Clone `odeon-backend` sources to `odeon-vagrant/www/` directory:

    git clone https://github.com/sorinbb/odeon-backend.git

Clone `odeon-frontend` sources to `odeon-vagrant/www/` directory:

    git clone https://github.com/sorinbb/odeon.git

Clone `odeon-backend-doc` sources to `odeon-vagrant/www/` directory:

    git clone https://github.com/sorinbb/odeon-backend-doc.git

Clone `elasticsearch-HQ` sources to `odeon-vagrant/www/` directory:

    git clone https://github.com/royrusso/elasticsearch-HQ.git

Clone `rockmongo` sources to `odeon-vagrant/www/` directory:

    git clone https://github.com/iwind/rockmongo.git

Install environment:

    vagrant up
    

## Tools

### Configure RockMongo

RockMongo is a MongoDB administration tool, written in PHP 5. [http://rockmongo.com](http://rockmongo.com)

    vagrant ssh
    
    cd /var/www/rockmongo
    
    composer update        
        
### Composer

Login to vagrant shell:

    vagrant ssh
    
Navigate to ``odeon-backend`` project directory:
    
    cd /var/www/odeon-backend
    
Update project bundles:
    
    composer update
           
    
## Manual environment components setup

Login to vagrant box:
    
    vagrant ssh
    
Switch to root (superuser):
    
    sudo su
    
Run entire environment provisioning:
    
    ansible-playbook -i 'localhost,' -c local /var/provision/ansible/vagrant.env.yml

Update virtual hosts:
    
    ansible-playbook -i 'localhost,' -c local /var/provision/ansible/app/vagrant/nginx-vhosts.yml

Create ``odeon`` elasticsearch index:
    
    ansible-playbook -i 'localhost,' -c local /var/provision/ansible/app/vagrant/elasticsearch-index.yml --extra-vars="elasticsearch_index=odeon" --tags="create"


## Update ``hosts`` file

Edit file:
 
    sudo nano /etc/hosts
    
Add vagrant host environment:
    
    192.168.33.208  doc-api.192.168.33.208.xip.io api.192.168.33.208.xip.io app.192.168.33.208.xip.io eshq.192.168.33.208.xip.io rockmongo.192.168.33.208.xip.io odeon.192.168.33.208.xip.io


## Vagrant commands

Install vagrant environment: 

    vagrant up

Access vagrant shell:

    vagrant ssh

Stop vagrant environment:

    vagrant halt


## Application commands
    
Login to vagrant box:
    
    vagrant ssh
    
Build frontend:
    
    ansible-playbook -i 'localhost,' -c local /var/provision/ansible/app/vagrant/app-build-frontend.yml

Build backend:
    
    ansible-playbook -i 'localhost,' -c local /var/provision/ansible/app/vagrant/app-build-backend.yml

