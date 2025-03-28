
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
    sudo apt-get update

    ##Configuramos el repositorio
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
    sudo chmod a+r /usr/share/keyrings/docker-archive-keyring.gpg
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

    #Actualizo los paquetes con los nuevos repositorios
    sudo apt-cache policy docker-ce
    sudo apt-get update -y
    #Instalo docker desde el repositorio oficial
    sudo apt-get -y  install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-compose

    #Lo configuro para que inicie en el arranque
    sudo systemctl enable docker


    #  ##INSTALAR DOCKER##
    # sudo apt-get install ca-certificates curl
    # sudo install -m 0755 -d /etc/apt/keyrings
    # sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
    # sudo chmod a+r /etc/apt/keyrings/docker.asc
    # echo \
    #    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
    #     $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
    #    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    # sudo apt-get update
    # sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    # ##CIERRO INSTALACION## 


    #####COPIAR ARCHIVOS DEL DIRECTORIO AL LINUX#####
    sudo chmod 775 /var/www/html
    sudo chown -R vagrant:vagrant /var/www/html
    sudo cp /vagrant/docker-compose.yml /var/www/html/docker-compose.yml

  SHELL
end
