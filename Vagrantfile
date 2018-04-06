#
# odeon-vagrant environment
#
Vagrant.configure(2) do |config|
    config.vm.box = 'ubuntu/trusty64'
    config.vm.hostname = 'odeon'
    config.vm.network 'private_network', ip: '192.168.33.208'
    config.vm.network "forwarded_port", guest: 2017, host: 2017, id: 'odeon-start'

    config.vm.synced_folder '.', '/vagrant', disabled: true
    config.vm.synced_folder './provision', '/var/provision', type: 'nfs', :nfs => { :mount_options => ['fmode=666'] }
    config.vm.synced_folder './www', '/var/www', type: 'nfs'

    config.ssh.forward_agent = true

    config.vm.provider 'virtualbox' do |vb|
        vb.name = 'odeon'
        vb.memory = '3096'
        vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'on']
        vb.customize ['modifyvm', :id, '--natdnsproxy1', 'on']
    end

    if Vagrant.has_plugin?('vagrant-vbguest') then
        config.vbguest.auto_update = false
    end

    config.vm.provision 'shell', privileged: true, inline: <<-SHELL
        echo "================================================================================";
        echo "Installing vagrant environment...";
        echo "================================================================================";
        bash /var/provision/bash/preinstall.sh
        ansible-playbook -i "localhost," -c local /var/provision/ansible/vagrant.env.yml
    SHELL

    config.vm.provision 'shell', run: 'always', inline: <<-SHELL, privileged: false
        echo "================================================================================";
        echo " ";
        echo " ";
        echo " ";
        echo " Machine IP address: 192.168.33.208";
        echo " Username: vagrant";
        echo " Password: vagrant";
        echo " ";
        echo " Or use 'vagrant ssh' command in order to login.";
        echo " ";
        echo " ";
        echo " Retailer APP: http://retailer.192.168.33.208.xip.io";
        echo " Admin APP: http://admin.192.168.33.208.xip.io";
        echo " API: http://api.192.168.33.208.xip.io";
        echo " API documentation: http://doc-api.192.168.33.208.xip.io";
        echo " ";
        echo " ";
        echo " ";
        echo "================================================================================";
    SHELL

end
