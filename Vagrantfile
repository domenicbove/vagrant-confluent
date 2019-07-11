Vagrant.configure("2") do |config|
  config.vm.define "master" do |subconfig|
    subconfig.vm.box = "centos/7"
    subconfig.vm.hostname = "master"
    subconfig.vm.network :private_network, ip: "10.0.0.10"
  end

  config.vm.define "slave" do |subconfig|
    subconfig.vm.box = "centos/7"
    subconfig.vm.hostname = "slave"
    subconfig.vm.network :private_network, ip: "10.0.0.11"
  end
end
