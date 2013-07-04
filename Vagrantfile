# -*- mode: ruby -*-
# vi: set ft=ruby :

personalization = File.expand_path("../Personalization", __FILE__)
load personalization

Vagrant.configure("2") do |config|
  config.vm.box = $base_box
  config.vm.box_url = $base_box_url

  config.vm.network :private_network, ip: $vm_ip
    config.vm.network :forwarded_port, guest: $vm_portforward_guest, host: $vm_portforward_host
    config.ssh.forward_agent = true

  config.vm.provider :virtualbox do |v|
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--memory", 1024]
    v.customize ["modifyvm", :id, "--name", $vhost]
  end

  config.vm.synced_folder "../", "/var/www"/vhosts/${vhost}, id: "vagrant-root"

  config.vm.provision :puppet do |puppet|
    puppet.manifests_path = "manifests"
    puppet.module_path = "modules"
    puppet.options = ['--verbose']
  end
end
