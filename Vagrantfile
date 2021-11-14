$script = <<-'SCRIPT'
echo setxkbmap fr > qwerty.sh
echo "@reboot /home/vagrant/qwerty.sh" > etc/crontab
chmod +x qwerty.sh 
sudo setxkbmap fr
sudo loadkeys fr
SCRIPT

Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  
  config.vm.define "target" do |target|    
    target.vm.box = "hashicorp/precise64"
    target.vm.network "private_network", ip: "192.168.60.10"
    #target.vm.network "forwarded_port", guest: 80, host: 8080
    #target.vm.provision "shell", inline: <<-SHELL
    #    apt-get update
    #    apt-get install -y apache2
    #SHELL
  end
  
  config.vm.define "attacker" do |attacker|
      attacker.vm.box = "kalilinux/rolling"
      attacker.vm.network "private_network", ip: "192.168.60.11"
      attacker.vm.provision "shell", inline: $script      
      #attacker.memory = "2048"
  end
  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
   

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
