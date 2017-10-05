# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  config.vm.box = "centos7"
  config.vm.synced_folder '.', '/vagrant', :disabled => true
  config.vm.provider :libvirt do |domain|
    domain.memory = 2048
  end
  config.vm.provision :ansible do |ansible|
    ansible.compatibility_mode = '2.0'
    ansible.playbook = ''
  end

  config.vm.define :ansiblesetup do |node|
    node.vm.network :private_network,
      :ip => '192.168.0.2',
      :prefix => '24',
      :libvirt__forward_mode => 'veryisolated',
      :libvirt__dhcp_enabled => false,
      :libvirt__network_name => 'tower_net'
    node.vm.provision :ansible do |ansible|
      ansible.playbook = 'ansiblesetup.yml'
    end
  end


  config.vm.define :redis1 do |node|
    node.vm.network :private_network,
      :ip => '192.168.0.8',
      :prefix => '24',
      :libvirt__forward_mode => 'veryisolated',
      :libvirt__dhcp_enabled => false,
      :libvirt__network_name => 'tower_net'
    node.vm.provision :ansible do |ansible|
      ansible.playbook = 'redis.yml'
      ansible.groups = {
        'redis-master' => ['redis1']
      }
    end
  end


  config.vm.define :redis2 do |node|
    node.vm.network :private_network,
      :ip => '192.168.0.9',
      :prefix => '24',
      :libvirt__forward_mode => 'veryisolated',
      :libvirt__dhcp_enabled => false,
      :libvirt__network_name => 'tower_net'
    node.vm.provision :ansible do |ansible|
      ansible.playbook = 'redis.yml'
      ansible.groups = {
        "redis-slave" => ['redis2']
      }
    end
  end


  config.vm.define :tower1 do |node|
    node.vm.network :private_network,
      :ip => '192.168.0.10',
      :prefix => '24',
      :libvirt__forward_mode => 'veryisolated',
      :libvirt__dhcp_enabled => false,
      :libvirt__network_name => 'tower_net'
    node.vm.provision :ansible do |ansible|
      ansible.playbook = 'centos.yml'
     ansible.groups = {
        "centoshosts" => ['tower1']
      }

    end
  end

  config.vm.define :tower2 do |node|
    node.vm.network :private_network,
      :ip => '192.168.0.11',
      :prefix => '24',
      :libvirt__forward_mode => 'veryisolated',
      :libvirt__dhcp_enabled => false,
      :libvirt__network_name => 'tower_net'
    node.vm.provision :ansible do |ansible|
      ansible.playbook = 'centos.yml'
      ansible.groups = {
        "centoshosts" => ['tower2']
      }


    end
  end

  config.vm.define :tower3 do |node|
    node.vm.network :private_network,
      :ip => '192.168.0.14',
      :prefix => '24',
      :libvirt__forward_mode => 'veryisolated',
      :libvirt__dhcp_enabled => false,
      :libvirt__network_name => 'tower_net'
    node.vm.provision :ansible do |ansible|
      ansible.playbook = 'centos.yml'
      ansible.groups = {
        "centoshosts" => ['tower3']
      }


    end
  end


  config.vm.define :postgres1 do |node|
    node.vm.network :private_network,
      :ip => '192.168.0.12',
      :prefix => '24',
      :libvirt__forward_mode => 'veryisolated',
      :libvirt__dhcp_enabled => false,
      :libvirt__network_name => 'tower_net'
    node.vm.provider :libvirt do |domain|
      domain.memory = 1024
    end


    node.vm.provision :ansible do |ansible|
      ansible.playbook = 'centos.yml'
      ansible.groups = {
        "centoshosts" => ['postgres1']
      }

    end

  end

  config.vm.define :postgres2 do |node|
    node.vm.network :private_network,
      :ip => '192.168.0.13',
      :prefix => '24',
      :libvirt__forward_mode => 'veryisolated',
      :libvirt__dhcp_enabled => false,
      :libvirt__network_name => 'tower_net'
    node.vm.provider :libvirt do |domain|
      domain.memory = 1024
    end

    node.vm.provision :ansible do |ansible|
      ansible.playbook = 'centos.yml'
      ansible.groups = {
        "centoshosts" => ['postgres2']
      }

    end

  end

end
