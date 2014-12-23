# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = '2'
VAGRANT_BOX = 'ubuntu-14.04-chef'
VAGRANT_BOX_URL = 'http://bit.ly/1qBrpXj'

Vagrant.require_version '>= 1.5.0'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.include_offline = true

  config.vm.define 'host1' do |cfg|
    cfg.vm.hostname = 'host1.domain'
    cfg.vm.box = VAGRANT_BOX
    cfg.vm.box_url = VAGRANT_BOX_URL
    cfg.vm.network 'private_network', ip: '172.28.128.3'
    cfg.vm.provision :chef_solo do |chef|
      chef.data_bags_path = 'data_bags'
      chef.cookbooks_path = 'cookbooks'
      chef.roles_path = 'roles'
      chef.encrypted_data_bag_secret_key_path = '.chef/encrypted_data_bag_secret'
      chef.custom_config_path = 'Vagrantfile.chef'
      chef.add_role('base')
    end
  end

  config.vm.define 'host2' do |cfg|
    cfg.vm.hostname = 'host2.domain'
    cfg.vm.box = VAGRANT_BOX
    cfg.vm.box_url = VAGRANT_BOX_URL
    cfg.vm.network 'private_network', ip: '172.28.128.4'
    cfg.vm.provision :chef_solo do |chef|
      chef.data_bags_path = 'data_bags'
      chef.cookbooks_path = 'cookbooks'
      chef.roles_path = 'roles'
      chef.encrypted_data_bag_secret_key_path = '.chef/encrypted_data_bag_secret'
      chef.custom_config_path = 'Vagrantfile.chef'
      chef.add_role('base')
    end
  end
end
