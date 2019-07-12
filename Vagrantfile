
Vagrant.configure("2") do |config|

  config.vm.define "broker1" do |broker1|
    broker1.vm.box = "centos/7"
    broker1.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end

    #broker1.vm.hostname = "broker1"
    broker1.vm.network "private_network", ip: "192.168.10.21"

    broker1.vm.network "forwarded_port", guest: 22, host: 2231
    broker1.ssh.guest_port = 2231

    broker1.vm.provision "shell" do |s|
      ## insert public key for easy ssh
      ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
      s.inline = <<-SHELL
        echo '192.168.10.21 broker1' >> /etc/hosts
        echo '192.168.10.22 broker2' >> /etc/hosts
        echo '192.168.10.23 broker3' >> /etc/hosts
        echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
        touch /etc/sysconfig/network
        sudo systemctl restart network
      SHELL
    end
  end

  config.vm.define "broker2" do |broker2|
    broker2.vm.box = "centos/7"
    broker2.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end

    #broker2.vm.hostname = "broker2"
    broker2.vm.network "private_network", ip: "192.168.10.22"

    broker2.vm.network "forwarded_port", guest: 22, host: 2232
    broker2.ssh.guest_port = 2232

    broker2.vm.provision "shell" do |s|
      ## insert public key for easy ssh
      ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
      s.inline = <<-SHELL
        echo '192.168.10.21 broker1' >> /etc/hosts
        echo '192.168.10.22 broker2' >> /etc/hosts
        echo '192.168.10.23 broker3' >> /etc/hosts
        echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
        touch /etc/sysconfig/network
        sudo systemctl restart network
      SHELL
    end
  end

  config.vm.define "broker3" do |broker3|
    broker3.vm.box = "centos/7"
    broker3.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end

    #broker3.vm.hostname = "broker3"
    broker3.vm.network "private_network", ip: "192.168.10.23"

    broker3.vm.network "forwarded_port", guest: 22, host: 2233
    broker3.ssh.guest_port = 2233

    broker3.vm.provision "shell" do |s|
      ## insert public key for easy ssh
      ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
      s.inline = <<-SHELL
        echo '192.168.10.21 broker1' >> /etc/hosts
        echo '192.168.10.22 broker2' >> /etc/hosts
        echo '192.168.10.23 broker3' >> /etc/hosts
        echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
        touch /etc/sysconfig/network
        sudo systemctl restart network
      SHELL
    end
  end


end
