$script = <<-'SCRIPT'
sudo setxkbmap fr
sudo sed -ie '/^XKBLAYOUT=/s/".*"/"fr"/' /etc/default/keyboard && udevadm trigger --subsystem-match=input --action=change
mkdir /home/vagrant/Desktop
mv /tmp/shell.php /home/vagrant/Desktop/
SCRIPT

$script2 = <<-'SCRIPT'
sudo loadkeys fr
sudo sed -ie '/^XKBLAYOUT=/s/".*"/"fr"/' /etc/default/keyboard && udevadm trigger --subsystem-match=input --action=change
sudo chmod 0600 ~/.ssh/authorized_keys
sudo apt-get update
sudo apt-get install -y apache2
sudo apt-get install -y libapache2-mod-php
sudo apt-get install -y python
sudo chmod u+s /usr/bin/python2.7
rm -r /var/www/html/*
mv /tmp/html/* /var/www/html
sudo chmod -R 777 /var/www/html/uploads/
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.define "target" do |target|    
    target.vm.box = "ubuntu/xenial64"
    target.vm.network "private_network", ip: "192.168.60.10"
    target.vm.provision "file", source: "./server", destination: "/tmp/html"
    target.vm.provision "shell", inline: $script2  
  end
  config.vm.define "attacker" do |attacker|
      attacker.vm.box = "kalilinux/rolling"
      attacker.vm.network "private_network", ip: "192.168.60.11"
      attacker.vm.provision "file", source: "./shell.php", destination: "/tmp/shell.php"
      attacker.vm.provision "shell", inline: $script
  end
end
