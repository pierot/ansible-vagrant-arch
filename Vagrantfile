# -*- mode: ruby -*-
# vi: set ft=ruby :

# Variables
$host_name = 'lokal'

# Boot script
$shell_boot = <<SCRIPT
  pacman -Sy --noconfirm python2
SCRIPT

# Version 2
Vagrant.configure("2") do |config|
  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "arch"

  # Hostname
  config.vm.hostname = $host_name

  # The url from where the 'config.vm.box' box will be fetched
  # if it doesn't already exist on the user's system.
  # config.vm.box_url = "https://googledrive.com/host/0B_BLFE4aPn5zUVpyaHdLanVnMTg/vagrant-archlinux-2013-8.box"

  # Create a forwarded port mapping which allows access to a
  # specific port within the machine from a port on the host machine.
  # In the example below, accessing "localhost:8080" will access
  # port 80 on the guest machine.
  config.vm.network :forwarded_port, guest: 80, host: 8080
  config.vm.network :forwarded_port, guest: 8888, host: 8181
  config.vm.network :forwarded_port, guest: 22, host: 3333, id: "ssh", auto_correct: true

  # Create a private network, which allows host-only access to
  # the machine using a specific IP.
  # config.vm.network :private_network, ip: "192.168.111.222"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make machine appear as physical device on your network
  # config.vm.network :public_network #, :bridge => "en1: Wi-Fi (AirPort)"

  # Setup basic things like python
  config.vm.provision :shell, :inline => $shell_boot

  config.vm.provision "ansible" do |ansible|
    ansible.inventory_path = "hosts.local"
    ansible.verbose = "vv" # Temporary?

    ansible.sudo = true

    # ansible.sudo_user = "vagrant" # dont do this, it breaks stuff
    # ansible.ask_sudo_pass = false # dont do this, it breaks stuff

    ansible.playbook = "bbdo-ansible-arch/site-vagrant.yml"
  end

  # The optional third argument is a set of non-required options.
  # config.vm.synced_folder "~/Downloads", "/home/pierot/tmp", owner: "pierot", group: "pierot"
  # config.vm.synced_folder "~/Dropbox/Work", "/home/pierot/work", owner: "pierot", group: "pierot"
  # config.vm.synced_folder "~/Documents/Projects", "/home/pierot/projects", owner: "pierot", group: "pierot"

  # The forward_agent option will allow you to use local SSH keys
  # to log in to remote services directly from the Vagrant/remote host.
  config.ssh.forward_agent = true

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  config.vm.provider :virtualbox do |vb|
    vb.name = $host_name

    # Don't boot with headless mode
    vb.gui = false

    # Use VBoxManage to customize the VM. For example to change memory:
    vb.customize ["modifyvm", :id, "--memory", "768"]
  end
end
