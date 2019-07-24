## install virtualbox
brew cask install virtualbox

## under system preferences allow the install
https://stackoverflow.com/questions/46546192/virtualbox-not-installing-on-high-sierra

## install vagrant
brew cask install vagrant

## only needed for debian 8, skip if otherwise
vagrant plugin install vagrant-vbguest

## vagrant up will create the vms, as well as generate an inventory file
vagrant up

## to start kerberos server and pull down keytabs run
ansible-playbook -i hosts.yml kerberos_server.yml

## run the cp-ansible
cd /path/to/cp-ansible

ansible-playbook -i ../vagrant-confluent/hosts.yml all.yml

ansible -i ../vagrant-confluent/hosts.yml all -m shell -a "systemctl --all | grep confluent"

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
