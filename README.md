##### Ansible Playbook for Elastic Cloud Enterprise (1.0.0-alpha4) infrastructure pre-requisites

* Somewhat-opinionated approach via Vagrant / Virtualbox, using bento/centos-7.1 for local testing with Virtualbox.

* Based on the Elastic's "Cover all of your bases" guide:
 https://www.elastic.co/guide/en/cloud-enterprise/1.0.0-alpha4/ece-configuring.html

* Playbook tested on CentOS 7.1 for Elastic Cloud Enterprise 1.0.0-alpha4 with Ansible 2.2.

##### Suggested usage
###### ansible.cfg:
```
[defaults]
inventory = ./hosts
callback_whitelist = profile_tasks
host_key_checking = False
```

###### Ansible Inventory
```
[elastic-cloud-enterprise]
### requires sshpass; install via OSX Homebrew: brew install https://raw.githubusercontent.com/kadwanev/bigboybrew/master/Library/Formula/sshpass.rb
127.0.0.1:2222 ansible_ssh_user=vagrant ansible_ssh_pass=vagrant
### OR Use the Private Key via Vagrant #${VAGRANT_MACHINE_DIR}/.vagrant/machines/default/virtualbox/private_key
#127.0.0.1:2222 ansible_ssh_user=vagrant ansible_ssh_private_key_file=${VAGRANT_MACHINE_DIR}/.vagrant/machines/default/virtualbox/private_key

```

###### Run playbook
```ansible-playbook -l elastic-cloud-enterprise elastic-cloud-enterprise.yml```
