# -*- mode: ruby -*-
# vi: set ft=ruby :

# Include our deploy command.
require File.dirname(__FILE__) + '/ssh-add.rb'

Vagrant::Config.run do |config|

  # Things you might want to modify!
  config.vm.host_name = "local"
  config.vm.customize ["modifyvm", :id, "--memory", "2048"]
  config.vm.network :hostonly, "33.33.33.40"

  config.vm.box = "precise-vbox-4.2.4"
  config.vm.box_url = "http://fattony.zivtech.com/files/precise-vbox-4.2.4.box"

  config.ssh.forward_agent = true

  config.vm.provision :puppet do |puppet|
    puppet.module_path = "puppet-modules"
    puppet.manifests_path = "puppet-manifests"
    puppet.manifest_file = "base.pp"
  end
  # NFS sharing does not work on windows, so if this is windows don't try to start it.
  require 'rbconfig'
  is_windows = (RbConfig::CONFIG['host_os'] =~ /mswin|mingw|cygwin/)
  if not is_windows
    config.vm.share_folder("web", "/var/www", "www", :nfs => true)
  else
    config.vm.share_folder("web", "/var/www", "www")
  end
end
