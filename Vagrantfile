box = "ubuntu16.04"
url = "https://cloud-images.ubuntu.com/xenial/current/xenial-server-cloudimg-amd64-vagrant.box"
#box = "ubuntu14.04"
#url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"
hostname = "iso-builder" 
domain = "builder.com" 
ip_address = "192.168.87.254"
ram = 2048

# you're doing.
Vagrant.configure(2) do |config|
  config.vm.box = box 
  config.vm.box_url = url
  config.vm.hostname = hostname + '.' + domain
  #config.vm.network "private_network", ip: ip_address 
  config.vm.network "public_network", ip: ip_address 
  config.ssh.insert_key = true
  #config.ssh.private_key_path = "~/.ssh/id_rsa"
  config.vbguest.auto_update = true
  config.vbguest.no_remote = false
  config.vbguest.auto_reboot = true
  config.vbguest.installer_arguments = %w{--nox11 --force}
  #config.vbguest.installer_arguments = %w{--nox11}
  #config.vbguest.iso_upload_path = "/tmp/Guest.iso"
  #config.vbguest.iso_mount_point = "/mnt/"
  
  config.vm.provider "virtualbox" do |vb|
    vb.customize [
      'modifyvm', :id,
      '--memory', ram
	vb.customize ["storagectl", :id, "--name", "IDEController", "--add", "ide"]
    vb.customize ["storageattach", :id, "--storagectl", "IDEController", "--port", "0", "--device", "0", "--type", "dvddrive", "--medium", "emptydrive"]      
    vb.customize ["modifyvm", :id, "--boot1", "disk", "--boot2", "dvd"]
    ]
  end

end
