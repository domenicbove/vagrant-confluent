## install virtualbox
brew cask install virtualbox

## under system preferences allow the install
https://stackoverflow.com/questions/46546192/virtualbox-not-installing-on-high-sierra

## install vagrant
brew cask install vagrant

## install vbguest vagrant plugin, only needed for debian 8, skip if otherwise
vagrant plugin install vagrant-vbguest

## open Vagrantfile and comment in which OS you would like to use for each vm (rhel7 is missing repos)
```
#BOX_BASE1 = "bento/debian-8"
#BOX_BASE2 = "generic/debian8"
#BOX_BASE3 = "debian/jessie64"
#BOX_BASE2 = "roboxes/rhel7"
BOX_BASE1 = "centos/7"
BOX_BASE2 = "centos/7"
BOX_BASE3 = "centos/7"
BOX_BASE4 = "centos/7"
#BOX_BASE2 = "bento/ubuntu-16.04"
```

## vagrant up will create 4 vms
vagrant up

## if you do not need kerberos, which is on node4
vagrant up node1 node2 node3

## to start kerberos server and pull down keytabs run
ansible-playbook -i inventories/kerberos.yml kerberos_server.yml

## run the cp-ansible
cd /path/to/cp-ansible

ansible-playbook -i ../vagrant-confluent/inventories/<security_type>.yml all.yml

## check services
ansible -i ../vagrant-confluent/inventories/<security_type>.yml preflight -m shell -a "systemctl --all | grep confluent"

## view control center
go to http://localhost:9021 or https://localhost:9021 in browser

## SSH into node 1,2,3,4
ssh vagrant@127.0.0.1 -o StrictHostKeyChecking=no -o IdentitiesOnly=yes -p 2231
ssh vagrant@127.0.0.1 -o StrictHostKeyChecking=no -o IdentitiesOnly=yes -p 2232
ssh vagrant@127.0.0.1 -o StrictHostKeyChecking=no -o IdentitiesOnly=yes -p 2233
ssh vagrant@127.0.0.1 -o StrictHostKeyChecking=no -o IdentitiesOnly=yes -p 2234

## for simplicity add this to .bash_profile
sshv1() {
  ssh vagrant@127.0.0.1 -o StrictHostKeyChecking=no -o IdentitiesOnly=yes -p 2231
}
sshv2() {
  ssh vagrant@127.0.0.1 -o StrictHostKeyChecking=no -o IdentitiesOnly=yes -p 2232
}
sshv3() {
  ssh vagrant@127.0.0.1 -o StrictHostKeyChecking=no -o IdentitiesOnly=yes -p 2233
}
sshv4() {
  ssh vagrant@127.0.0.1 -o StrictHostKeyChecking=no -o IdentitiesOnly=yes -p 2234
}

## clean up a node
vagrant destroy node4 -f

## destroy everything
vagrant destroy -f
