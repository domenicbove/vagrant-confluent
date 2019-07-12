
Vagrant.configure("2") do |config|

  config.vm.define "broker1" do |broker1|
    broker1.vm.box = "centos/7"
    broker1.vm.hostname = "broker1"
    #broker1.vm.network "private_network", ip: "192.168.56.11"

    config.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end
  end

  config.vm.define "broker2" do |broker2|
    broker2.vm.box = "centos/7"
    broker2.vm.hostname = "broker2"
    #broker2.vm.network "private_network", ip: "192.168.56.11"

    config.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end
  end

  # config.vm.define "broker3" do |broker3|
  #   broker3.vm.box = "centos/7"
  #   broker3.vm.hostname = "broker3"
  #   #broker2.vm.network "private_network", ip: "192.168.56.11"
  #
  #   config.vm.provider "virtualbox" do |vb|
  #     vb.memory = 2048
  #     vb.cpus = 2
  #   end
  # end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "hello.yml"
    ansible.host_vars = {
      "broker1" => {"kafka.broker.id" => 1},
      "broker2" => {"kafka.broker.id" => 2}
    }
    ansible.groups = {
      "all:vars" => {
        "ansible_ssh_common_args" => "-o StrictHostKeyChecking=no -o IdentitiesOnly=yes",
        "security_mode" => "plaintext",
        "ansible_become" => "true"
      },
      "preflight" => ["broker[1:2]"],
      "zookeeper" => ["broker[1:2]"],
      "broker" => ["broker[1:2]"]

    }
  end

end
