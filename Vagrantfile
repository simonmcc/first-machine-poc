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
  config.vm.box = "boot-from-iso"
  config.vm.box_url = "https://www.dropbox.com/s/yum30836kjwgt4w/boot-from-iso.box?dl=1"

  config.vm.provider "virtualbox" do |virtualbox|
    virtualbox.gui = true unless ENV['NO_GUI']
    # --boot<1-4> none|floppy|dvd|disk|net>
    virtualbox.customize ["modifyvm", :id, "--boot1", "dvd"]
    # VBoxManage.exe storageattach "<uuid|vmname>" --storagectl IDE --port 0 --device 0 --type dvddrive --medium "X:\Folder\containing\the.iso"
    virtualbox.customize ["storageattach", :id, "--storagectl",
                            "IDE", "--port",  "0", "--device", "0", "--type", "dvddrive",
                            "--medium", "/tmp/Custom1404.iso"]
  end

end
