VAGRANTFILE_API_VERSION = "2"
 Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
	config.vm.box = "ubuntu/trusty64"
	config.vm.provider "virtualbox" do |v|
	 v.customize ["modifyvm", :id, "--memory", "2048", "--cpus", "2"]
  	config.vm.provision "ansible" do |ansible|
	ansible.playbook = "plays/fluentd.yml"
	ansible.groups = { 
	"client-d" => ["lvclient1","lvclient2"],
	"logservers" => ["lvm"],
}
	end
	 end
	config.vm.define "lvm" do |lvm|
  	lvm.vm.hostname = "lvm" 
	lvm.vm.network  :private_network, ip: "172.16.13.121",  virtualbox__intnet: true 
	lvm.vm.network "forwarded_port", guest: 80, host: 8000
	end
	config.vm.define "lvclient1" do |lvclient1|
  	lvclient1.vm.hostname = "lv-client1"
	lvclient1.vm.network :private_network,  ip: "172.16.13.122",  virtualbox__intnet: true
	end
	config.vm.define "lvclient2" do |lvclient2|
	lvclient2.vm.hostname = "lv-client2"
	lvclient2.vm.network :private_network, ip: "172.16.13.123",  virtualbox__intnet: true
	end
 end
