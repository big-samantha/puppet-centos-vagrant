# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "centos-65-x64-vbox436-nocm"

  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  config.vm.box_url = "http://puppet-vagrant-boxes.puppetlabs.com/centos-65-x64-virtualbox-nocm.box"

  config.vm.synced_folder "src/", "/root/src/"

    # Write a fragment to /etc/profile.d that activates envpuppet
    config.vm.provision :shell, :inline => <<-EOS
tee /etc/profile.d/envpuppet.sh << "EOF"
export ENVPUPPET_BASEDIR=/root/src
eval $($ENVPUPPET_BASEDIR/puppet/ext/envpuppet)
EOF
    EOS

    # The puppet user and group are required to run Puppet 2.7.0 -- 3.1.0.
    config.vm.provision :shell, :inline => <<-EOS
groupadd puppet
useradd puppet -g puppet
    EOS

config.vm.provision "shell",
  inline: 'yum groupinstall "Development Tools" -y'

config.vm.provision "shell",
  inline: 'yum install ruby rubygems ruby-devel -y'

config.vm.provision "shell",
  inline: 'gem install json'

end
