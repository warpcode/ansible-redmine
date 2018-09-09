# -*- mode: ruby -*-
# vi: set ft=ruby :

PROJECTNAME = "redmine"
NETWORK_PRIVATE_IP_PREFIX = "172.16.3.%d"

$OCTET_START = 1

Vagrant.configure("2") do |config|
    boxes = [
        {
            'hostname' => 'ubuntu-17.10',
            'box' => 'bento/ubuntu-17.10'
        }
    ]

    boxes.each do |value|
        ip_address = NETWORK_PRIVATE_IP_PREFIX % [$OCTET_START]
        hostname = PROJECTNAME + '-' + value ['hostname']

        $OCTET_START = $OCTET_START + 1

        config.vm.define "#{hostname}" do |node|
            node.vm.box = value['box']
            node.vm.hostname = hostname
            node.vm.network :private_network, ip: ip_address
            node.vm.boot_timeout = 600

            # Virtualbox settings
            node.vm.provider :virtualbox do |v|
                v.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/vagrant-root", "1"]
                v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
                v.customize ["modifyvm", :id, "--natdnsproxy1",        "on"]
                v.customize ["modifyvm", :id, "--memory", 512]
                # v.customize ["modifyvm", :id, "--cpuexecutioncap", '50']
                v.customize ["modifyvm", :id, "--name", hostname]

                # Options to get nested VM's working
                v.customize ["modifyvm", :id, "--cableconnected1", "on"]
                # v.customize ["modifyvm", :id, "--hwvirtex", "off"]
                v.customize ["modifyvm", :id, "--cpus", 2]
            end

            node.vm.provision "ansible_local" do |ansible|
                ansible.playbook = "tests/test.yml"
                ansible.extra_vars = {
                    ansible_connection: 'local'
                }
            end
        end
    end
end
