VAGRANTFILE_API_VERSION = "2"

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-18.04"

  config.vm.provider :virtualbox do |v|
    v.memory = 2048
    v.cpus = 2
  end

  config.vm.define "www" do |www|
    www.vm.hostname = "www.test"
    # for debugging / local connection to database
    # www.vm.network :forwarded_port, guest: 5432, host: 5432
    # www.vm.network :forwarded_port, guest: 8080, host: 8080
    www.vm.network :private_network, ip: "192.168.33.10"
  end

  config.vm.provision "ansible" do |ansible|
     ansible.limit = "all"
     ansible.verbose  = true
     ansible.playbook = "provisioning/playbook.yml"
     ansible.inventory_path = "provisioning/inventory"
     ansible.extra_vars = {
        ansible_ssh_user: 'vagrant',
        ansible_ssh_private_key_file: "~/.vagrant.d/insecure_private_key"}
  end
end
