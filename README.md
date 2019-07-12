
## vagrant up will create the vms, as well as generate an inventory file
vagrant up

## inventory file found at this path
ansible-playbook -i hosts.yml ../cp-ansible-internal/all.yml

ansible -i hosts.yml all -m shell -a "systemctl --failed"

## SSH into broker 1,2,3
ssh vagrant@127.0.0.1 -o StrictHostKeyChecking=no -o IdentitiesOnly=yes -p 2231
ssh vagrant@127.0.0.1 -o StrictHostKeyChecking=no -o IdentitiesOnly=yes -p 2232
ssh vagrant@127.0.0.1 -o StrictHostKeyChecking=no -o IdentitiesOnly=yes -p 2233



## OLD
ansible-playbook -i ./.vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory ../cp-ansible-internal/all.yml



## OLD
ssh -i /Users/dbove/workspace/vagrant-gettingstarted/.vagrant/machines/broker1/virtualbox/private_key vagrant@127.0.0.1 -p 2222 -o StrictHostKeyChecking=no -o IdentitiesOnly=yes

ssh -i /Users/dbove/workspace/vagrant-gettingstarted/.vagrant/machines/broker2/virtualbox/private_key vagrant@127.0.0.1 -p 2201 -o StrictHostKeyChecking=no -o IdentitiesOnly=yes
