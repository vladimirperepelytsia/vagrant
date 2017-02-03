# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

require 'yaml'
params = YAML.load_file("config.yml")

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'ubuntu/trusty64'

  config.vm.network "forwarded_port", guest: params["forwarded_port_guest"], host: params["forwarded_port_host"]
  config.vm.network "private_network", ip: params["private_network"]

  # config.ssh.forward_agent = true
  localaliases = []
  if params["projects"]
    params["projects"].each do |project|
      localaliases << project["name"];
      Dir.mkdir(project["local_path"]) unless File.exists?(project["local_path"])
      config.vm.synced_folder project["local_path"], project["virtual_path"], type: 'nfs'
    end
  end
  
  if localaliases.length > 0
    #config.vm.hostname = "example-box-hostname"
    config.hostmanager.enabled = true
    config.hostmanager.manage_host = true
    config.hostmanager.aliases = localaliases
  end

  #Copy files from the host machine to the guest machine
  config.vm.provision "file", source: params["id_rsa_path"], destination: "/home/vagrant/.ssh/id_rsa"

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
    vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'on']
  end
    



  # ansible provision
  config.vm.provision 'ansible' do |ansible|
    ansible.playbook = './playbook.yml'
  end
end
