#BOX_BASE1 = "bento/debian-8"
#BOX_BASE2 = "generic/debian8"
#BOX_BASE3 = "debian/jessie64"
#BOX_BASE2 = "roboxes/rhel7"
BOX_BASE1 = "centos/7"
BOX_BASE2 = "centos/7"
BOX_BASE3 = "centos/7"
BOX_BASE4 = "centos/7"
#BOX_BASE2 = "bento/ubuntu-16.04"

Vagrant.configure("2") do |config|

  # Speed up networking
  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--nictype1", "virtio" ]
    v.customize ["modifyvm", :id, "--nictype2", "virtio" ]
    v.customize ["modifyvm", :id, "--natdnshostresolver4", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy4", "on"]
  end

  config.vm.define "node1" do |node1|
    node1.vm.box = BOX_BASE1
    node1.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end

    node1.vm.hostname = "node1.example.com"
    node1.vm.network "private_network", ip: "192.168.10.21"

    node1.vm.network "forwarded_port", guest: 22, host: 2231
    node1.ssh.guest_port = 2231

    node1.vm.provision "shell" do |s|
      ## insert public key for easy ssh
      ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
      s.inline = <<-SHELL
        sed -i '/node1.example.com/d' /etc/hosts
        echo '192.168.10.21 node1.example.com' >> /etc/hosts
        echo '192.168.10.22 node2.example.com' >> /etc/hosts
        echo '192.168.10.23 node3.example.com' >> /etc/hosts
        echo '192.168.10.24 node4.example.com' >> /etc/hosts
        echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
        # touch /etc/sysconfig/network
        # sudo systemctl restart network
      SHELL
    end
  end

  config.vm.define "node2" do |node2|
    node2.vm.box = BOX_BASE2
    node2.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end

    node2.vm.hostname = "node2.example.com"
    node2.vm.network "private_network", ip: "192.168.10.22"

    ## Run control center
    node2.vm.network "forwarded_port", guest: 9021, host: 9021

    node2.vm.network "forwarded_port", guest: 22, host: 2232
    node2.ssh.guest_port = 2232

    node2.vm.provision "shell" do |s|
      ## insert public key for easy ssh
      ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
      s.inline = <<-SHELL
        sed -i '/node2.example.com/d' /etc/hosts
        echo '192.168.10.21 node1.example.com' >> /etc/hosts
        echo '192.168.10.22 node2.example.com' >> /etc/hosts
        echo '192.168.10.23 node3.example.com' >> /etc/hosts
        echo '192.168.10.24 node4.example.com' >> /etc/hosts
        echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
        # touch /etc/sysconfig/network
        # sudo systemctl restart network
      SHELL
    end
  end

  config.vm.define "node3" do |node3|
    node3.vm.box = BOX_BASE3
    node3.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end

    node3.vm.hostname = "node3.example.com"
    node3.vm.network "private_network", ip: "192.168.10.23"

    ## Run ksql
    node3.vm.network "forwarded_port", guest: 8088, host: 8088

    node3.vm.network "forwarded_port", guest: 22, host: 2233
    node3.ssh.guest_port = 2233

    node3.vm.provision "shell" do |s|
      ## insert public key for easy ssh
      ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
      s.inline = <<-SHELL
        sed -i '/node3.example.com/d' /etc/hosts
        echo '192.168.10.21 node1.example.com' >> /etc/hosts
        echo '192.168.10.22 node2.example.com' >> /etc/hosts
        echo '192.168.10.23 node3.example.com' >> /etc/hosts
        echo '192.168.10.24 node4.example.com' >> /etc/hosts
        echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
        touch /etc/sysconfig/network
        sudo systemctl restart network
      SHELL
    end
  end

  config.vm.define "node4" do |node4|
    node4.vm.box = BOX_BASE4
    node4.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 1
    end

    node4.vm.hostname = "node4.example.com"
    node4.vm.network "private_network", ip: "192.168.10.24"

    node4.vm.network "forwarded_port", guest: 22, host: 2234
    node4.ssh.guest_port = 2234

    node4.vm.provision "shell" do |s|
      ## insert public key for easy ssh
      ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
      s.inline = <<-SHELL
        sed -i '/node4/d' /etc/hosts
        echo '192.168.10.21 node1.example.com' >> /etc/hosts
        echo '192.168.10.22 node2.example.com' >> /etc/hosts
        echo '192.168.10.23 node3.example.com' >> /etc/hosts
        echo '192.168.10.24 node4.example.com' >> /etc/hosts
        echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
        touch /etc/sysconfig/network
        sudo systemctl restart network
      SHELL
    end
  end

end
