# -*- mode: ruby -*-
# vi: set ft=ruby :
#

$script = <<SCRIPT
    chmod 600 /home/vagrant/.ssh/id_rsa
    chmod 644 /home/vagrant/.ssh/id_rsa.pub
    rpm -q ansible || yum -y install ansible
SCRIPT

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "CentOS64x86_64"

  # Port forwarding for Jenkins
  config.vm.network "forwarded_port", guest: 8080, host: 8080

  # plant my ssh keys
  config.vm.provision "file" , source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/id_rsa.pub"
  config.vm.provision "file" , source: "~/.ssh/id_rsa"    , destination: "~/.ssh/id_rsa"

  config.vm.provision "shell" do |s|
    s.inline     = $script
    s.privileged = true
  end
end
