Vagrant.configure("2") do |config|
    # Configure the box to use
    config.vm.box       = 'precise64'

    config.vm.provider "vmware_fusion" do |v, override|
        override.vm.box     = 'hashicorp/precise64'
    end

    # Configure the network interfaces
    config.vm.network :private_network, ip:    "192.168.33.10"
    config.vm.network :forwarded_port,  guest: 80,    host: 8080
    config.vm.network :forwarded_port,  guest: 8081,  host: 8081
    config.vm.network :forwarded_port,  guest: 3306,  host: 3306
    config.vm.network :forwarded_port,  guest: 27017, host: 27017

    # Configure shared folders
    config.vm.synced_folder ".",  "/vagrant", id: "vagrant-root", :mount_options => ['dmode=777', 'fmode=777'] #, :nfs=>true
    config.vm.synced_folder "..", "/var/www", id: "application", group: "www-data", owner: "www-data", :mount_options => ['dmode=777', 'fmode=777'] #, :nfs=>true

    # Configure VirtualBox environment
    config.vm.provider :virtualbox do |v|
        v.name = (0...8).map { (65 + rand(26)).chr }.join
        v.customize [ "modifyvm", :id, "--memory", 2048 ]
    end

    # Configure VMWare Fusion environment
    config.vm.provider :vmware_fusion do |v|
        v.name = (0...8).map { (65 + rand(26)).chr }.join
        v.vmx["memsize"] = "2048"
    end

    # Provision the box
    config.vm.provision :ansible do |ansible|
        ansible.playbook = "ansible/site.yml"
    end
end
