Vagrant.configure("2") do |config|
    config.vm.provision "shell", inline: <<-SHELL
        apt-get update -y
        echo "192.168.66.10  ansible-master" >> /etc/hosts
        echo "192.168.66.11  ansible-host01" >> /etc/hosts
        echo "192.168.66.12  ansible-host02" >> /etc/hosts
    SHELL
    
    config.vm.define "ansible" do |ansible|
      ansible.vm.box = "bento/ubuntu-22.04"
      ansible.vm.hostname = "ansible-master"
      ansible.vm.network "private_network", ip: "192.168.66.10"
      ansible.vm.provider "virtualbox" do |vb|
          vb.memory = 4048
          vb.cpus = 2
      end
      ansible.vm.provision "shell", inline: <<-SHELL
      sudo apt install ansible -y
  SHELL
    end
  
    (1..2).each do |i|
  
    config.vm.define "ansible-host0#{i}" do |target|
      target.vm.box = "bento/ubuntu-22.04"
      target.vm.hostname = "ansible-host0#{i}"
      target.vm.network "private_network", ip: "192.168.66.1#{i}"
      target.vm.provider "virtualbox" do |vb|
          vb.memory = 2048
          vb.cpus = 1
      end
    end
    
    end
  end
  
  