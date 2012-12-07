chef-neo4j
==========

Prequisites:
--------------
  - Install Vagrant ruby gem with VirtualBox
  - Install chef ruby gem
  - Install librarian ruby gem

Step 1: Install vagrant box:
----------------------------

  $ vagrant init

   Then add to Vagrantfile:

    config.vm.box = "opscode-ubuntu-12.04"
    config.vm.box_url = "https://opscode-vm.s3.amazonaws.com/vagrant/boxes/opscode-ubuntu-12.04.box" 

    
Step 2: Install Cheffile
-------------------------

  $ librarian-chef init


Step 3: Add cookbooks
-----------------------



Edit Cheffile:

    cookbook 'apt'
    cookbook 'neo4j-server', :git => 'http://github.com/michaelklishin/neo4j-server-chef-cookbook'


Step 4: Download cookbooks
---------------------------
  $ librarian-chef install



Step 5: Prepare provision VM
-----------------------------


  Vagrantfile
    
    config.vm.provision :chef_solo do |chef|
      chef.cookbooks_path = "cookbooks"
      chef.add_recipe "apt"
      chef.add_recipe "neo4j-server::tarball"
    end
    
  
Step 6: Provision VM
----------------------

vagrant up

   .... provisioning takes a while ....


Step 7: Finish
---------------

    vagrant ssh

