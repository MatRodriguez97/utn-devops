
Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/jammy64"
  config.vm.network "private_network", ip: "192.168.33.10"  
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.hostname = "utn-devops.localhost"

  # Redirecciono puertos desde la maquina virtual a la maquina real. Por ejemplo.
  config.vm.network "forwarded_port", guest: 8082, host: 8082, auto_correct: true
  # Puerto en que escuchar el servidor maestro de Puppet
  config.vm.network "forwarded_port", guest: 8140, host: 8140, auto_correct: true
  
  
  #Permite descargas con certificados vencidos o por http
  config.vm.box_download_insecure = true
  
  # configuración del nombre de maquina
  config.vm.hostname = "utn-devops.localhost"
  config.vm.boot_timeout = 3600
  
  #descripcion de la VM
  config.vm.provider "virtualbox" do |v|
	  v.name = "DevOps-puppet"
    v.memory = "1024"
  end
  
  # Mapeo de directorios que se comparten entre la maquina virtual y nuestro equipo. En este caso es
  # el propio directorio donde está el archivo  y el directorio "/vagrant" dentro de la maquina virtual.
  config.vm.synced_folder ".", "/vagrant"

  config.vm.provision "file", source: "hostConfigs/ufw", destination: "/tmp/utw"
  config.vm.provision "file", source: "hostConfigs/etc_hosts.txt", destination: "/tmp/etc_hosts.txt"
  # Archivos de Puppet
  config.vm.provision "file", source: "hostConfigs/puppet/site.pp", destination: "/tmp/site.pp"
  config.vm.provision "file", source: "hostConfigs/puppet/init.pp", destination: "/tmp/init.pp"
  config.vm.provision "file", source: "hostConfigs/puppet/init_jenkins.pp", destination: "/tmp/init_jenkins.pp"
  config.vm.provision "file", source: "hostConfigs/puppet/puppet-master.conf", destination: "/tmp/puppet-master.conf"
  config.vm.provision "file", source: "hostConfigs/puppet/.env", destination: "/tmp/env"
  # En este archivo tendremos el provisionamiento de software necesario para nuestra
  # maquina virtual. Por ejemplo, servidor web, servidor de base de datos, etc.
  config.vm.provision :shell, path: "Vagrant.bootstrap.sh", run: "always"

end
  