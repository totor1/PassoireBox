$script = <<-'SCRIPT'
sudo setxkbmap fr
sudo loadkeys fr
SCRIPT

Vagrant.configure("2") do |config|
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

end
