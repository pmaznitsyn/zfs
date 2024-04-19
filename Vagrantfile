# -*- mode: ruby -*-
# vim: set ft=ruby :

MACHINES = {
  :zfs => {
        :box_name => "generic/alma8",
        :ip_addr => '192.168.56.101',
	:disks => {
		:sata1 => {
			:dfile => './sata1.vdi',
			:size => 100,
			:port => 1
		},
		:sata2 => {
                        :dfile => './sata2.vdi',
                        :size => 100, # Megabytes
			:port => 2
		},
                :sata3 => {
                        :dfile => './sata3.vdi',
                        :size => 100,
                        :port => 3
                },
                :sata4 => {
                        :dfile => './sata4.vdi',
                        :size => 100, # Megabytes
                        :port => 4
                },
                :sata5 => {
                        :dfile => './sata5.vdi',
                        :size => 100, # Megabytes
                        :port => 5 
                },
                :sata6 => {
    		        :dfile => './sata6.vdi',
		        :size => 100,
    		        :port => 6
	        },
	        :sata7 => {
    		        :dfile => './sata7.vdi',
		        :size => 100, 
    		        :port => 7
	        },
	        :sata8 => {
    		        :dfile => './sata8.vdi',
		        :size => 100, 
    		        :port => 8
	        }
	}	
  },
}

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|

      if Vagrant.has_plugin?("vagrant-vbguest") then
        config.vbguest.auto_update = false
      end
      config.vm.define boxname do |box|

          box.vm.box = boxconfig[:box_name]
          box.vm.host_name = boxname.to_s

          box.vm.network "private_network", ip: boxconfig[:ip_addr]

          box.vm.provider :virtualbox do |vb|
            	  vb.customize ["modifyvm", :id, "--memory", "1024"]
                  needsController = false
		  boxconfig[:disks].each do |dname, dconf|
			  unless File.exist?(dconf[:dfile])
				vb.customize ['createhd', '--filename', dconf[:dfile], '--variant', 'Fixed', '--size', dconf[:size]]
                                needsController =  true
                          end

		  end
                   boxconfig[:disks].each do |dname, dconf|
                       vb.customize ['storageattach', :id,  '--storagectl', 'SATA Controller', '--port', dconf[:port], '--device', 0, '--type', 'hdd', '--medium', dconf[:dfile]]
                  end
          end
          config.vm.provision "shell", path: "setup_zfs.sh"
      end
  end
end
