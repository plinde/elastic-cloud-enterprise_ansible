##### Ansible Playbook for Elastic Cloud Enterprise (1.0.0-alpha4) infrastructure pre-requisites

* Based on the Elastic's "Cover all of your bases" guide:
 https://www.elastic.co/guide/en/cloud-enterprise/1.0.0-alpha4/ece-configuring.html

* Playbook tested on CentOS 7.1 for Elastic Cloud Enterprise 1.0.0-alpha4 with Ansible 2.2.

* Simple Vagrantfile based on bento/centos-7.1 for local testing with Virtualbox.

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
10.0.0.2:22
10.0.0.3:22
10.0.0.4:22
```

###### Run playbook
```ansible-playbook -i hosts -l elastic-cloud-enterprise elastic-cloud-enterprise.yml```
