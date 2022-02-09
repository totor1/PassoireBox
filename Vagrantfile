$script = <<-'SCRIPT'
sudo setxkbmap fr
sudo loadkeys fr
sudo sed -ie '/^XKBLAYOUT=/s/".*"/"fr"/' /etc/default/keyboard && udevadm trigger --subsystem-match=input --action=change
SCRIPT

$script2 = <<-'SCRIPT'
sudo chmod 0600 ~/.ssh/authorized_keys
sudo apt-get update
sudo apt-get install -y apache2
sudo apt-get install -y libapache2-mod-php
sudo setxkbmap fr
sudo loadkeys fr
sudo sed -ie '/^XKBLAYOUT=/s/".*"/"fr"/' /etc/default/keyboard && udevadm trigger --subsystem-match=input --action=change
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.define "target" do |target|    
    target.vm.box = "ubuntu/xenial64"
    target.vm.network "private_network", ip: "192.168.60.10"
    #target.vm.network "forwarded_port", guest: 80, host: 8080
    target.vm.provision "shell", inline: $script2
    target.vm.provision "file", source: "./server", destination: "/tmp/html"
    target.vm.provision "shell", inline: "rm /var/www/html/index.html; mv /tmp/html/* /var/www/html"
  end
  config.vm.define "attacker" do |attacker|
      attacker.vm.box = "kalilinux/rolling"
      attacker.vm.network "private_network", ip: "192.168.60.11"
      attacker.vm.provision "shell", inline: $script      
      #attacker.memory = "2048"
  end
#
end
