
Vagrant.configure("2") do |config|

  # config.vm.define "jumpbox" do |jumpbox|
  #   jumpbox.vm.box = "centos/7"
  #   jumpbox.vm.provider "virtualbox" do |vb|
  #     vb.memory = 1024
  #     vb.cpus = 1
  #   end
  #
  #   jumpbox.vm.hostname = "jumpbox"
  #   jumpbox.vm.network "private_network", ip: "192.168.10.20"
  #
  #   jumpbox.vm.network "forwarded_port", guest: 22, host: 2230
  #   jumpbox.ssh.guest_port = 2230
  #
  #   jumpbox.vm.provision "shell" do |s|
  #     ## insert public key for easy ssh
  #     ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
  #     ssh_priv_key = File.readlines("#{Dir.home}/.ssh/id_rsa").first.strip
  #     s.inline = <<-SHELL
  #       echo '192.168.10.21 node1' >> /etc/hosts
  #       echo '192.168.10.22 node2' >> /etc/hosts
  #       echo '192.168.10.23 node3' >> /etc/hosts
  #       echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
  #       echo #{ssh_pub_key} > /home/vagrant/.ssh/id_rsa.pub
  #       echo #{ssh_priv_key} > /home/vagrant/.ssh/id_rsa
  #       echo 'sshv() { ssh vagrant@$1 -o StrictHostKeyChecking=no -o IdentitiesOnly=yes ; }' >> /home/vagrant/.bash_profile
  #       touch /etc/sysconfig/network
  #       sudo systemctl restart network
  #     SHELL
  #   end
  # end

  config.vm.define "node1" do |node1|
    node1.vm.box = "centos/7"
    node1.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end

    node1.vm.hostname = "node1"
    node1.vm.network "private_network", ip: "192.168.10.21"

    node1.vm.network "forwarded_port", guest: 22, host: 2231
    node1.ssh.guest_port = 2231

    node1.vm.provision "shell" do |s|
      ## insert public key for easy ssh
      ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
      s.inline = <<-SHELL
        sed -i '/node1/d' /etc/hosts
        echo '192.168.10.21 node1' >> /etc/hosts
        echo '192.168.10.22 node2' >> /etc/hosts
        echo '192.168.10.23 node3' >> /etc/hosts
        echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
        touch /etc/sysconfig/network
        sudo systemctl restart network
      SHELL
    end
  end

  config.vm.define "node2" do |node2|
    node2.vm.box = "centos/7"
    node2.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end

    node2.vm.hostname = "node2"
    node2.vm.network "private_network", ip: "192.168.10.22"

    ## Run control center
    node2.vm.network "forwarded_port", guest: 9021, host: 9021

    node2.vm.network "forwarded_port", guest: 22, host: 2232
    node2.ssh.guest_port = 2232

    node2.vm.provision "shell" do |s|
      ## insert public key for easy ssh
      ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
      s.inline = <<-SHELL
        sed -i '/node2/d' /etc/hosts
        echo '192.168.10.21 node1' >> /etc/hosts
        echo '192.168.10.22 node2' >> /etc/hosts
        echo '192.168.10.23 node3' >> /etc/hosts
        echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
        touch /etc/sysconfig/network
        sudo systemctl restart network
      SHELL
    end
  end

  config.vm.define "node3" do |node3|
    node3.vm.box = "centos/7"
    node3.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end

    node3.vm.hostname = "node3"
    node3.vm.network "private_network", ip: "192.168.10.23"

    ## Run ksql
    node3.vm.network "forwarded_port", guest: 8088, host: 8088

    node3.vm.network "forwarded_port", guest: 22, host: 2233
    node3.ssh.guest_port = 2233

    node3.vm.provision "shell" do |s|
      ## insert public key for easy ssh
      ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
      s.inline = <<-SHELL
        sed -i '/node3/d' /etc/hosts
        echo '192.168.10.21 node1' >> /etc/hosts
        echo '192.168.10.22 node2' >> /etc/hosts
        echo '192.168.10.23 node3' >> /etc/hosts
        echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
        touch /etc/sysconfig/network
        sudo systemctl restart network
      SHELL
    end
  end

  # config.vm.define "node4" do |node4|
  #   node4.vm.box = "centos/7"
  #   node4.vm.provider "virtualbox" do |vb|
  #     vb.memory = 1024
  #     vb.cpus = 1
  #   end
  #
  #   node4.vm.hostname = "node4"
  #   node4.vm.network "private_network", ip: "192.168.10.24"
  #
  #   node4.vm.network "forwarded_port", guest: 22, host: 2234
  #   node4.ssh.guest_port = 2234
  #
  #   node4.vm.provision "shell" do |s|
  #     ## insert public key for easy ssh
  #     ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
  #     s.inline = <<-SHELL
  #       sed -i '/node4/d' /etc/hosts
  #       echo '192.168.10.21 node1' >> /etc/hosts
  #       echo '192.168.10.22 node2' >> /etc/hosts
  #       echo '192.168.10.23 node3' >> /etc/hosts
  #       echo '192.168.10.24 node4' >> /etc/hosts
  #       echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
  #       touch /etc/sysconfig/network
  #       sudo systemctl restart network
  #     SHELL
  #   end
  # end


end
