# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "precise64"
  #config.vm.customize ["modifyvm", :id, "--memory", "768"]
  config.vm.provider :lxc do |lxc|
    lxc.customize 'cgroup.memory.limit_in_bytes', '1024M'
  end
  config.vm.define :lxc do |lxc_config|
    lxc_config.vm.network :forwarded_port, guest: 80, host: 3000
    lxc_config.vm.provision :shell, inline:
    'echo "Replace this with your puppet manifests"'
  end
  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  config.vm.box_url = "http://dl.dropbox.com/u/13510779/lxc-precise-amd64-2013-05-08.box"

  # Boot with a GUI so you can see the screen. (Default is headless)
  # config.vm.boot_mode = :gui

  # Assign this VM to a host-only network IP, allowing you to access it
  # via the IP. Host-only networks can talk to the host machine as well as
  # any other machines on the same network, but cannot be accessed (through this
  # network interface) by any external networks.
  # config.vm.network :hostonly, "192.168.33.10"

  # Assign this VM to a bridged network, allowing you to connect directly to a
  # network using the host's network device. This makes the VM appear as another
  # physical device on your network.
  # config.vm.network :bridged

  # Forward a port from the guest to the host, which allows for outside
  # computers to access the VM, whereas host only networking does not.
  # config.vm.forward_port "web", 80, 8333

  # Share an additional folder to the guest VM. The first argument is
  # an identifier, the second is the path on the guest to mount the
  # folder, and the third is the path on the host to the actual folder.
  #  config.vm.share_folder "v-data", "/vagrant_data", "../data"

   config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = "./cookbooks"
    #chef.log_level = :debug
    chef.json = {
      "mysql" => {
        "server_root_password" => "typo3",
	"server_debian_password" => "typo3",
	"server_repl_password" => "typo3"
      }
    }
    chef.add_recipe("typo3")
    chef.add_recipe("mysql::server")
   end

end
