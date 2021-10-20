# -*- mode: ruby -*-
# vim: set ft=ruby :

MACHINES = {
  :master => {
        :box_name => "generic/centos8",
        :ip_addr => '10.13.1.101',
        :memory => 256
  },
  :slave => {
        :box_name => "generic/centos8",
        :ip_addr => '10.13.1.102',
        :memory => 256
  }
  }

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|

      config.vm.define boxname do |box|
          box.vm.box = boxconfig[:box_name]
          box.vm.host_name = boxname.to_s
          box.vm.network "private_network", ip: boxconfig[:ip_addr]

          box.vm.provider :virtualbox do |vb|
            vb.customize ["modifyvm", :id, "--memory", boxconfig[:memory]]
          end
          
          box.vm.provision "shell", inline: <<-SHELL
      mkdir -p ~root/.ssh; cp ~vagrant/.ssh/auth* ~root/.ssh


          SHELL
		  # box.vm.provision :ansible do |ansible|
		  #   ansible.playbook = "./ansible/playbook.yml"
			# ansible.inventory_path = "./ansible/inventory.yml"
			# ansible.verbose = true
		  # end

      end
  end
end