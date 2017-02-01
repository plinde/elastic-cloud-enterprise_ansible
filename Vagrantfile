Vagrant.configure("2") do |config|
  config.vm.box = "bento/centos-7.1"
  config.vm.network "public_network"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "8192"
  end
  config.persistent_storage.enabled = true
  config.persistent_storage.location = "./data-volume.vdi"
  config.persistent_storage.size = 5000
  config.persistent_storage.mountname = 'data'
  config.persistent_storage.filesystem = 'xfs'
  config.persistent_storage.mountpoint = '/mnt/data'
  config.persistent_storage.volgroupname = 'data-volgroup'
  config.persistent_storage.mountoptions = ['defaults', 'pquota', 'prjquota']
end
