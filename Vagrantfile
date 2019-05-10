# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
Vagrant.configure("2") do |config|

  ## vagrant-cachier configuration
  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :machine
  end

  ## SSH settings
  # Do not auto-generate an insecure SSH key (keep the default).
  # Indicates local private ssh-key as first option to be used by Vagrant.
  config.ssh.insert_key = false
  config.ssh.private_key_path = ["~/.ssh/id_rsa",
                                 "~/.vagrant.d/insecure_private_key"]

  # Copy your public key as authorized key into the host,
  # allowing passwordless access for the vagrant user
  config.vm.provision "file",
                      run: 'once',
                      source: "~/.ssh/id_rsa.pub",
                      destination: "~/.ssh/authorized_keys"

  # Limit memory on host
  config.vm.provider :virtualbox do |vb|
    vb.memory = 256
  end

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  {
    'paul'   => '192.168.33.10',
    'john'   => '192.168.33.11',
    'george' => '192.168.33.12',
    'ringo'  => '192.168.33.13',
  }.each do |short_name, ip|
    config.vm.define short_name do |host|
      #host.vm.box = "centos/7"
      host.vm.box = "bento/centos-7"
      host.vm.hostname = "#{short_name}"
      host.vm.network :private_network, ip: ip
    end
  end

end
