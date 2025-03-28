
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
    #apt-get install -y apache2
    #sudo chmod 775 /var/www/html
    #sudo chown -R vagrant:vagrant /var/www/html
    #sudo cp /vagrant/index.html /var/www/html/index.html 

    #Instalamos los paquetes de docker
    cu#rl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
    sudo chmod a+r /usr/share/keyrings/docker-archive-keyring.gpg
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

    #Actualizo los paquetes con los nuevos repositorios
    sudo apt-cache policy docker-ce
    sudo apt-get update -y
    #Instalo docker desde el repositorio oficial
    sudo apt-get -y  install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-compose

    #Lo configuro para que inicie en el arranque
    sudo systemctl enable docker

    #Entramos a la carpeta raiz del compose y levantamos el mismo
    cd /vagrant && sudo docker compose up -d

  SHELL
end
  