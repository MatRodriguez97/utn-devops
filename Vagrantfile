
Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/jammy64"
  config.vm.network "private_network", ip: "192.168.33.10"  
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.hostname = "utn-devops.localhost"

  config.vm.provider "virtualbox" do |v|
	  v.name = "DevOps"
    v.memory = "1024"
  end
  
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y apache2
    sudo chmod 775 /var/www/html
    sudo chown -R vagrant:vagrant /var/www/html
    sudo cp /vagrant/index.html /var/www/html/index.html 
  SHELL
end
