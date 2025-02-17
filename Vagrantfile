Vagrant.configure("2") do |config|
  # Attacker VM (Kali Linux)
  config.vm.define "attacker" do |attacker|
    attacker.vm.box = "kalilinux/rolling"
    attacker.vm.network "private_network", ip: "192.168.56.10"
    # Default credentials: username: vagrant, password: vagrant (SSH key used automatically)
  end

  # Target VM (Metasploitable2)
  config.vm.define "target" do |target|
    target.vm.box = "rapid7/metasploit2"
    target.vm.network "private_network", ip: "192.168.56.20"
    # Override SSH defaults since Metasploitable2 uses different credentials:
    target.ssh.username = "msfadmin"
    target.ssh.password = "msfadmin"
    target.ssh.insert_key = false
  end

  # Firewall/IPS VM (Ubuntu with Suricata)
  config.vm.define "firewall" do |fw|
    fw.vm.box = "bento/ubuntu-20.04"
    fw.vm.network "private_network", ip: "192.168.56.30"
    fw.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update
      sudo apt-get install -y software-properties-common
      sudo add-apt-repository universe -y
      sudo apt-get update
      sudo add-apt-repository ppa:oisf/suricata-stable -y
      sudo apt-get update
      sudo apt-get install -y suricata
      # Optionally enable IPS mode (if desired):
      # sudo sed -i 's/block: false/block: true/' /etc/suricata/suricata.yaml
      # sudo systemctl restart suricata
    SHELL
  end
end
