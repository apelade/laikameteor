# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network :forwarded_port, host: 3000, guest: 3000
  config.vm.synced_folder '.', '/laikameteor'
  config.vm.provider "virtualbox" do |v|
    v.memory = 4096
    v.cpus = 2
  end


  config.vm.provision "chef_solo" do |chef|

    chef.add_recipe "meteor"
    chef.add_recipe "nodejs"
    chef.add_recipe "apt"
    chef.add_recipe "build-essential"
    chef.add_recipe "yum"


    #chef.add_recipe "phantomjs"
    #### phantomjs windows cookbooks libs: #####
    #### comment out chocolatey from phantomjs/metadata.rb if win support not needed
    #chef.add_recipe "chocolatey"
    #chef.add_recipe "build-essential"
    #chef.add_recipe "powershell"
    #chef.add_recipe "windows"
    #chef.add_recipe "chef_handler"
    #chef.add_recipe "ms_dotnet2"
    #chef.add_recipe "ms_dotnet4"
    #chef.add_recipe "ms_dotnet45"

  end

  config.vm.provision "shell", inline: "apt-get install -y phantomjs"
  config.vm.provision "shell", inline: "npm install -g laika"
  config.vm.provision "shell", inline: "pkill -f mongod"
  config.vm.provision "shell", inline: "mkdir -p /data/db/"
  config.vm.provision "shell", inline: "sudo chown -R vagrant:vagrant /data/"
  config.vm.provision "shell", inline: "mkdir -p log"
  config.vm.provision "shell", inline: "mongod --fork --logpath log/mongodb.log --smallfiles --nojournal"
  config.vm.provision "shell", inline: "laika"  

end

