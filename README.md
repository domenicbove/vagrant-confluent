## vagrant up will create the vms, as well as generate an inventory file
vagrant up

## run the ansible install
cd /path/to/cp-ansible-internal

ansible-playbook -i ../vagrant-confluent/local-hosts.yml all.yml

ansible -i ../vagrant-confluent/local-hosts.yml all -m shell -a "systemctl --all | grep confluent"

## SSH into node 1,2,3
ssh vagrant@127.0.0.1 -o StrictHostKeyChecking=no -o IdentitiesOnly=yes -p 2231
ssh vagrant@127.0.0.1 -o StrictHostKeyChecking=no -o IdentitiesOnly=yes -p 2232
ssh vagrant@127.0.0.1 -o StrictHostKeyChecking=no -o IdentitiesOnly=yes -p 2233

## SSH into the jumphost, which can ssh to all
ssh vagrant@127.0.0.1 -o StrictHostKeyChecking=no -o IdentitiesOnly=yes -p 2230
ssh vagrant@node1
