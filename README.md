## vagrant up will create the vms, as well as generate an inventory file
vagrant up

## inventory file found at this path
cd /path/to/cp-ansible-internal

ansible-playbook -i ../vagrant-confluent/hosts.yml all.yml

ansible -i ../vagrant-confluent/hosts.yml all -m shell -a "systemctl --failed"

## SSH into node 1,2,3
ssh vagrant@127.0.0.1 -o StrictHostKeyChecking=no -o IdentitiesOnly=yes -p 2231
ssh vagrant@127.0.0.1 -o StrictHostKeyChecking=no -o IdentitiesOnly=yes -p 2232
ssh vagrant@127.0.0.1 -o StrictHostKeyChecking=no -o IdentitiesOnly=yes -p 2233

## SSH into the jumphost, which can ssh to all
ssh vagrant@127.0.0.1 -o StrictHostKeyChecking=no -o IdentitiesOnly=yes -p 2230
ssh vagrant@node1
