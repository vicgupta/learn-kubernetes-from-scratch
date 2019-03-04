# How to install using Vagrant

There are two scripts that must be used with Vagrant.
* Vagrantfile - file for vagrant to configure the multiple masters and nodes
* install-kubeadm.sh - file to install the kubeadm, kubelet, kubectl


Below is the vagrant script that you can run with ```vagrant up``` 
```
ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure(2) do |config|

    config.vm.provision "shell", path: "install-kubeadm.sh"

    MasterCount = 1

    (1..MasterCount).each do |i|
        config.vm.define "master#{i}" do |master|
            master.vm.box = "ubuntu/bionic64"
            master.vm.hostname = "master#{i}.dev.local"
            master.vm.network "private_network", ip: "192.168.0.1#{i}"
            master.vm.provider "virtualbox" do |v|
                v.name = "master#{i}"
                v.memory = 2048
                v.cpus = 2
            end
        #node.vm.provision "shell", path: "bootstrap_kworker.sh"
        end  
    end
    NodeCount = 1

    (1..NodeCount).each do |i|
        config.vm.define "node#{i}" do |node|
            node.vm.box = "ubuntu/bionic64"
            node.vm.hostname = "kworker#{i}.dev.local"
            node.vm.network "private_network", ip: "192.168.0.1#{i}"
            node.vm.provider "virtualbox" do |v|
                v.name = "node#{i}"
                v.memory = 1024
                v.cpus = 1
            end
        end
        #node.vm.provision "shell", path: "bootstrap_kworker.sh"
    end
end
```

The other is the install-kubeadm.sh script to be placed in the same directory as the Vagrantfile
```
sudo apt update
sudo apt install git -y
sudo git clone http://github.com/vicgupta/xenial-shell
cd xenial-shell
bash kubeadm.sh
```
