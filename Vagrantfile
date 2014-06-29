# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "saucy-64-server"

  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/saucy/current/saucy-server-cloudimg-amd64-vagrant-disk1.box"

  # config.vm.box_check_update = false

  config.ssh.forward_agent = true

  config.vm.network "private_network", ip: "10.10.10.30"
  config.vm.hostname = "vagrant.puppet-box.com"

  config.vm.synced_folder "shared/", "/shared"
  config.vm.synced_folder "puppet", "/etc/puppet", :mount_options => ["dmode=777,fmode=777"]

  config.vm.provision "puppet" do |puppet|
    puppet.manifests_path = "puppet/manifests"
    puppet.module_path = "puppet/modules"
    puppet.manifest_file  = "site.pp"
    puppet.options = "--fileserverconfig=/vagrant/puppet/fileserver.conf"
    puppet.facter = {
        "fqdn" => "vagrant.puppet-box.com",
    }
  end

end
