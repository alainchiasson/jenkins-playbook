# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

 N = 3
 (1..N).each do |machine_id|
   config.vm.define "node-#{machine_id}" do |machine|

     machine.vm.hostname = "node-#{machine_id}"
     machine.vm.box = "centos/7"
     machine.vm.network "private_network", type: "dhcp"
     machine.vm.provider "virtualbox" do |vb|
       vb.memory = "1024"
     end


     # Only execute once the Ansible provisioner,
     # when all the machines are up and ready.
     if machine_id == N
       machine.vm.provision :ansible do |ansible|

         ansible.groups = {
           "master" => ["node-1"],
           "slaves" => ["node-2","node-3"]
         }

         ansible.limit = "all"
         ansible.playbook = "playbook.yml"
       end
     end
   end
 end
end
