##################################################
# Vagrant Configuration
##################################################

Vagrant.require_version ">= 1.8.1"

ENV['PYTHONIOENCODING'] = "utf-8"

Vagrant.configure("2") do |config|

    config.vm.provider :virtualbox do |v|
        v.name = "php56box.vb"
        v.customize [
            "modifyvm", :id,
            "--name", "php56box.vb",
            "--memory", 2048,
            "--natdnshostresolver1", "on",
            "--cpus", 1,
        ]
    end

    config.vm.hostname = "php56box.vb"
    config.vm.box = "ubuntu/trusty64"

    config.vm.network :private_network, ip: "10.10.10.11"
    config.ssh.forward_agent = true
    config.ssh.pty = true
    config.ssh.insert_key = false

    #############################################################
    # Ansible initial provisioning
    #############################################################

    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/playbook.yml"
        ansible.inventory_path = "ansible/inventories/dev"
        ansible.limit = 'all'
        ansible.extra_vars = {
            private_interface: "10.10.10.11",
            hostname: "php56box.vb"
        }
    end
end
