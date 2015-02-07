# -*- mode: ruby -*-
# vi: set ft=ruby :
#
# vagrant box add CentOS64x86_64 https://github.com/2creatives/vagrant-centos/releases/download/v6.4.2/centos64-x86_64-20140116.box
# git clone
# vagrant up

`ssh-add -l`

if not $?.success?
  puts 'Your SSH does not currently contain any keys (or is stopped.)'
  puts 'Please start it and add your Github SSH key to continue.'  
  exit 1
end

if not File.directory?("./dotfiles")
    `git clone git@github.com:jayrajput/dotfiles.git`
end

$script = <<SCRIPT
    # move this to the ansible
    /vagrant/dotfiles/install.py

    rpm -q ansible || sudo yum -y install ansible

    # vagrant mounts all the file with mode=777.
    # ansible have problem using hosts file with mode=777
    # so copy the hosts file and change mode to 666
    cp /vagrant/hosts /tmp/hosts
    chmod 666 /tmp/hosts

    sudo ansible-playbook -i/tmp/hosts /vagrant/setup.yml
SCRIPT

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "CentOS64x86_64"

  # SSH agent forwarding, useful for cloning git repo on the vm
  # config.ssh.forward_agent = true

  config.vm.provision "shell" do |s|
    s.inline     = $script
    s.privileged = false
  end
end
