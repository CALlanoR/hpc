# -*- mode: ruby -*-
# vim: ft=ruby


# ---- Configuration variables ----

GUI               = false # Enable/Disable GUI
RAM               = 500   # Default memory size in MB

# Network configuration
DOMAIN            = ".example.com"
NETWORK           = "192.168.56."
NETMASK           = "255.255.255.0"

# Default Virtualbox .box
# See: https://wiki.debian.org/Teams/Cloud/VagrantBaseBoxes
BOX               = 'ubuntu/trusty64'


HOSTS = {
  "hpcmaster" => [NETWORK+"110", RAM, GUI, BOX, "master.sh"],
  "hpcnode1"  => [NETWORK+"111", RAM, GUI, BOX, "node.sh" ],
  "hpcnode2"  => [NETWORK+"112", RAM, GUI, BOX, "node.sh" ],
  "hpcnode3"  => [NETWORK+"113", RAM, GUI, BOX, "node.sh" ],  
}

# ---- Vagrant configuration ----

Vagrant.configure(2) do |config|
  HOSTS.each do | (name, cfg) |
    ipaddr, ram, gui, box, provisioning_script = cfg

    config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"
    config.vm.define name do |machine|
      machine.vm.box   = box
      machine.vm.guest = :ubuntu
      machine.vm.provision :shell, path: provisioning_script

      machine.vm.provider "virtualbox" do |vbox|
        vbox.gui    = gui
        vbox.memory = ram
        vbox.name = name
      end

      machine.vm.hostname = name + DOMAIN
      machine.vm.network 'private_network', ip: ipaddr, netmask: NETMASK, name: 'vboxnet0', adapter:2
    end


  end # HOSTS-each

end
