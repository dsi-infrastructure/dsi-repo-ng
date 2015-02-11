# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu14.04-chef"
  config.vm.box_url = "http://bit.ly/1pK1sQ8"
  config.vm.hostname = "test.toriki.srv.gov.pf"

  # Personalisation du provider : virtualbox
  config.vm.provider "virtualbox" do |v|
    v.gui = true
    v.name = "test"
    v.memory = 512
    v.cpus = 1
  end

  # Configuration reseau:
  config.vm.network "private_network", ip: "192.168.7.29"

  # chef-solo installation:
  #config.vm.provision :shell, inline: "export DEBIAN_FRONTEND=noninteractive; apt-get install chef -y"

  # Provisionner un serveur aggregator avec chef-solo:
  config.vm.provision "chef_solo" do |chef|
    chef.custom_config_path = "Vagrantfile.chef"
    chef.cookbooks_path = ["cookbooks"]
    chef.cookbooks_path = ["cookbooks.dev"]
    chef.roles_path = "roles"
    chef.data_bags_path=["data_bags"]
    chef.encrypted_data_bag_secret_key_path = "secret_key"

#   chef.add_role("base")
#   chef.add_role("owncloud")

   #chef.add_recipe "apt::default"

   # avant, modifier les attributs par defaut:
    chef.json = {
      "chef-nodeAttributes" => {
#        "databag_name" => [
#          "cron",
#          "clusters",
#          "chef-iptables"
#        ]
        "databag_name" => {
          "roleName" => "lvm",
          "roleNames" => [
            "iscsi",
            "qmail"
          ],
          "names" => {
            "roleName" => "chef-iptables",
            "roleNames" => [
              "iscsi",
              "qmail"
            ],
          }
        }
      }
    }

    chef.run_list = [
        "recipe[chef-nodeAttributes::default]",
#        "recipe[chef-hostsfile::default]",
#        "recipe[chef-lvm::default]",
#        "recipe[sysctl::apply]",
#        "recipe[limits::default]",
#        "recipe[chef-squid_ldap_auth::default]",
#        "recipe[apache2::mod_php5]",
#        "recipe[chef-squidGuard::default]",
#        "recipe[squid::default]",
#        "recipe[chef-haproxy-ng::default]",
#        "recipe[keepalived::default]",
#        "recipe[chef-delegate::default]",
#        "recipe[chef-awstats::default]",
#        "recipe[chef-iptables::default]",
#        "recipe[apt-cacher-ng]",
#        "recipe[chef-crontab::create]"
#        "recipe[chef-iscsi::default]"
#        "recipe[chef-crontab::create]"
#        "recipe[tomcat::default]"
         "recipe[chef-tomcat-application::default]"
    ]


  end

end
