# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.

  config.vm.define "iso-builder" do |iso_builder|
    # this VM is used to build the ISO, when your developing on an OSX machine
    # apply the iso-builder role to create a custom install ISO
    iso_builder.vm.box = "hashicorp/precise64"

    iso_builder.vm.provision :shell, inline: "cp /vagrant/mini.iso /tmp/mini.iso"
    iso_builder.vm.provision :shell, inline: "[[ ! -f /tmp/hos2.0-build01-399.iso ]] && cp /vagrant/hos2.0-build01-399.iso /tmp/ || exit 0"
    iso_builder.vm.provision "ansible" do |ansible|
      ansible.playbook = "build_iso.yml"
    end
    iso_builder.vm.provision :shell, inline: "cp /tmp/Custom.iso /vagrant/Custom.iso"
  end

  config.vm.define "boot-from-iso" do |iso_boot|
    # this VM is a special unprovisioned node that we set to boot from an ISO
    iso_boot.vm.box = "boot-from-iso"
    iso_boot.vm.box_url = "https://www.dropbox.com/s/yum30836kjwgt4w/boot-from-iso.box?dl=1"

    iso_boot.vm.provider "virtualbox" do |virtualbox|
      virtualbox.gui = true unless ENV['NO_GUI']
      # --boot<1-4> none|floppy|dvd|disk|net>
      virtualbox.customize ["modifyvm", :id, "--boot1", "dvd"]
      # VBoxManage.exe storageattach "<uuid|vmname>" --storagectl IDE --port 0 --device 0 --type dvddrive --medium "X:\Folder\containing\the.iso"
      virtualbox.customize ["storageattach", :id, "--storagectl",
                              "IDE", "--port",  "0", "--device", "0", "--type", "dvddrive",
                              "--medium", "Custom.iso"]
    end
  end

end
