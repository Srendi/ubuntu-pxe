box = "ubuntu/xenial64"
#box = "ubuntu16.04"
#url = "https://cloud-images.ubuntu.com/xenial/current/xenial-server-cloudimg-amd64-vagrant.box"
#box = "ubuntu14.04"
#url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"
hostname = "iso-builder" 
domain = "homelan.local" 
ip_address = "192.168.50.254"
ram = 2048
cpus = 1

# you're doing.
Vagrant.configure(2) do |config|
  #config.vm.box_check_update = false
  config.vm.box = box 
  #config.vm.box_url = url
  config.vm.hostname = hostname + '.' + domain
  #config.vm.network "private_network", ip: ip_address 
  config.vm.network "public_network", ip: ip_address 
  config.ssh.insert_key = true
  #config.ssh.private_key_path = "~/.ssh/id_rsa"
  #
  # Install Latest VBoxGuestAdditions
  #config.vbguest.iso_path = "http://download.virtualbox.org/virtualbox/5.1.8/VBoxGuestAdditions_5.1.8.iso"
  config.vbguest.iso_upload_path = "/tmp/VBoxGuestAdditions_5.1.8.iso"
  config.vbguest.iso_mount_point = "/mnt/"
  config.vbguest.auto_update = true
  config.vbguest.auto_reboot = true
  config.vbguest.no_install = false
  config.vbguest.no_remote = false
  #
  config.vm.provider "virtualbox" do |vb|
    vb.customize [
      'modifyvm', :id,
      '--memory', ram ]
    vb.customize [
      'modifyvm', :id,
      '--cpus', cpus ]
	#
	#Add an empty cdrom
    vb.customize ["storageattach", :id, "--storagectl", "IDE", "--port", "0", "--device", "0", "--type", "dvddrive", "--medium", "emptydrive"]
    vb.customize ["modifyvm", :id, "--boot1", "disk", "--boot2", "dvd"]
  end

end
