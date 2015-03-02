# -*- mode: ruby -*-
# vi: set ft=ruby :
#
# vagrant box add CentOS64x86_64 https://github.com/2creatives/vagrant-centos/releases/download/v6.4.2/centos64-x86_64-20140116.box
# git clone
# vagrant up

$script = <<SCRIPT
    rpm -q ansible || yum -y install ansible
SCRIPT

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "CentOS64x86_64"

  # Port forwarding for Jenkins
  config.vm.network "forwarded_port", guest: 8080, host: 8080

  config.vm.provision "shell" do |s|
    s.inline     = $script
    s.privileged = true
  end
end
