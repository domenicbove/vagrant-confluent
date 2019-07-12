
## vagrant up will create the vms, as well as generate an inventory file
vagrant up

## inventory file found at this path
ansible-playbook -i ./.vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory ../cp-ansible-internal/all.yml
