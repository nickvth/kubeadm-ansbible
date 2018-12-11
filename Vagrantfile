Vagrant.configure(2) do |config|
     # Setup virtual machine box. This VM configuration code is always executed.
    config.vm.box = "generic/centos7"

    config.vm.define "kubemaster1" do |kubemaster1|
        kubemaster1.vm.network "private_network", ip: "10.10.43.10"
        kubemaster1.vm.hostname = 'kubemaster1'
        kubemaster1.vm.provision "shell", inline:
          'echo "10.10.43.10 kubemaster1" > /etc/hosts'
    end

    config.vm.define "worker1" do |worker1|
        worker1.vm.network "private_network", ip: "10.10.43.11"
        worker1.vm.hostname = 'worker1'
        worker1.vm.provision "shell", inline:
          'echo "10.10.43.11 worker1" > /etc/hosts'
    end

    config.vm.define "worker2" do |worker1|
      worker1.vm.network "private_network", ip: "10.10.43.12"
      worker1.vm.hostname = 'worker2'
      worker1.vm.provision "shell", inline:
        'echo "10.10.43.12 worker2" > /etc/hosts'
    end 

    config.vm.define "worker3" do |worker1|
      worker1.vm.network "private_network", ip: "10.10.43.13"
      worker1.vm.hostname = 'worker3'
      worker1.vm.provision "shell", inline:
        'echo "10.10.43.13 worker1" > /etc/hosts'
    end

    config.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 2048]
      v.customize ["modifyvm", :id, "--cpus", 2]
      v.customize ["modifyvm", :id, "--ioapic", "on"]
      v.customize ["modifyvm", :id, "--rtcuseutc", "off"]
    end

    config.ssh.forward_agent = true 

end