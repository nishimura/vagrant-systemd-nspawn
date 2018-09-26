# -*- mode: ruby -*-
# vi: set ft=ruby :

if not ENV['VAGRANT_BRIDGE_DEV']
  puts 'VAGRANT_BRIDGE_DEV required.'
  abort
end
if not ENV['VAGRANT_ETH1_IP']
  puts 'VAGRANT_ETH1_IP required.'
  abort
end
if not ENV['VAGRANT_HOST_NAME']
  puts 'VAGRANT_HOST_NAME required.'
  abort
end

Vagrant.configure("2") do |config|
  config.vm.box = "debian/stretch64"

  interfaces = %x(VBoxManage list bridgedifs)
  re         = /Name: +(.*#{ENV['VAGRANT_BRIDGE_DEV']}.*)/
  if interfaces =~ re
    config.vm.network "public_network", ip: ENV['VAGRANT_ETH1_IP'], bridge: $1
  else
    config.vm.network "private_network", ip: ENV['VAGRANT_ETH1_IP']
  end

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
  end

  config.vm.hostname = "#{ENV['VAGRANT_HOST_NAME']}"

  config.vm.synced_folder "data", "/host_data"
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.persistent_storage.enabled = true
  config.persistent_storage.location = "container/btrfs.vdi"
  config.persistent_storage.size = 20 * 1000
  config.persistent_storage.format = false
  config.persistent_storage.partition = false

  config.vm.provision "shell", inline: <<-SHELL
    sudo mkdir -p ~/.ssh
    sudo chmod 700 ~/.ssh
    sudo cp /host_data/authorized_keys ~/.ssh/authorized_keys
  SHELL

  # override Vagrant ip setting
  config.vm.provision "shell", inline: "systemctl restart systemd-networkd && systemctl restart systemd-networkd", run: 'always'

end
