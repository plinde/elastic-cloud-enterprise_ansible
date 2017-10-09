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
### requires sshpass; install via OSX Homebrew:
### brew install https://raw.githubusercontent.com/kadwanev/bigboybrew/master/Library/Formula/sshpass.rb
127.0.0.1:2222 ansible_ssh_user=vagrant ansible_ssh_pass=vagrant
### OR Use the Private Key via Vagrant #${VAGRANT_MACHINE_DIR}/.vagrant/machines/default/virtualbox/private_key
#127.0.0.1:2222 ansible_ssh_user=vagrant ansible_ssh_private_key_file=${VAGRANT_MACHINE_DIR}/.vagrant/machines/default/virtualbox/private_key

```

###### Run playbook
```ansible-playbook -l elastic-cloud-enterprise elastic-cloud-enterprise.yml```

###### Docker save/load (for multi-node quick installs, without need for local Docker Registry cache)
```
docker pull docker.elastic.co/cloud-enterprise/elastic-cloud-enterprise:1.0.0-alpha4

docker save docker.elastic.co/cloud-enterprise/elastic-cloud-enterprise:1.0.0-alpha4 --output docker.elastic.co_cloud-enterprise_elastic-cloud-enterprise:1.0.0-alpha4.tar

### Ideally, host this somewhere where your other nodes can pull it down quickly
# python -m SimpleHTTPServer 8080
# wget http://somehost:8080/docker.elastic.co_cloud-enterprise_elastic-cloud-enterprise:1.0.0-alpha4.tar

docker load --input docker.elastic.co_cloud-enterprise_elastic-cloud-enterprise:1.0.0-alpha4.tar

export PUBLIC_IP=$(ip address show  enp0s8 | grep 'inet ' | sed -e 's/^.*inet //' -e 's/\/.*$//')
wget https://download.elasticsearch.org/cloud/elastic-cloud-enterprise-installer.sh
bash -x elastic-cloud-enterprise-installer.sh --host-storage-path /mnt/data --public-host-name ${PUBLIC_IP} --host-ip ${PUBLIC_IP} --debug

export HOST_IP=$(ip address show  enp0s8 | grep 'inet ' | sed -e 's/^.*inet //' -e 's/\/.*$//')
bash <(curl -fsSL https://download.elastic.co/cloud/elastic-cloud-enterprise.sh) install

### Docker 'nuke' if something goes wrong and you need to quickly wipe your containers
# docker ps -a | awk '{print $1}' | xargs docker kill; docker ps -a | awk '{print $1}' | xargs docker rm

```
