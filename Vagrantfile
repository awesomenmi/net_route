# -*- mode: ruby -*-
# vim: set ft=ruby :

MACHINES = {

  :R1 => {
    :box_name => "centos/7",
    :net => [
              {adapter: 2, auto_config: false, virtualbox__intnet: "vlan12"},
              {adapter: 3, auto_config: false, virtualbox__intnet: "vlan13"},
              {ip: '10.1.0.1', adapter: 4, netmask: "255.255.255.0", virtualbox__intnet: "AR0"},
            ]
  }, 

  :R2 => {
    :box_name => "centos/7",
    :net => [
              {adapter: 2, auto_config: false, virtualbox__intnet: "vlan12"},
              {adapter: 3, auto_config: false, virtualbox__intnet: "vlan23"},
              {ip: '10.2.0.1', adapter: 4, netmask: "255.255.255.0", virtualbox__intnet: "AR1"},
            ]
  }, 

  :R3 => {
    :box_name => "centos/7",
    :net => [
              {adapter: 2, auto_config: false, virtualbox__intnet: "vlan13"},
              {adapter: 3, auto_config: false, virtualbox__intnet: "vlan23"},
              {ip: '10.3.0.1', adapter: 4, netmask: "255.255.255.0", virtualbox__intnet: "AR2"},
            ]
  }, 


}

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|
      
    config.vm.define boxname do |box|

        box.vm.box = boxconfig[:box_name]
        box.vm.host_name = boxname.to_s

        config.vm.provider "virtualbox" do |v|
          v.memory = 256
        end

        boxconfig[:net].each do |ipconf|
          box.vm.network "private_network", ipconf
        end
        
        if boxconfig.key?(:public)
          box.vm.network "public_network", boxconfig[:public]
        end

        box.vm.provision "shell", inline: <<-SHELL
          mkdir -p ~root/.ssh
                cp ~vagrant/.ssh/auth* ~root/.ssh
        SHELL
        
        case boxname.to_s

          when "R1"
            box.vm.provision "shell", run: "always", inline: <<-SHELL
              setenforce 0
              yum install -y quagga
              cp /vagrant/network-scripts/ifcfg-vlan12-r1 /etc/sysconfig/network-scripts/ifcfg-vlan12
              cp /vagrant/network-scripts/ifcfg-vlan13-r1 /etc/sysconfig/network-scripts/ifcfg-vlan13
              cp /vagrant/network-scripts/daemons /etc/quagga/daemons
              cp /vagrant/network-scripts/r1-zebra.conf /etc/quagga/zebra.conf
              cp /vagrant/network-scripts/r1-ospfd.conf /etc/quagga/ospfd.conf
              chown quagga:quaggavt /etc/quagga/ospfd.conf
              chown quagga:quagga /etc/quagga/zebra.conf
              echo net.ipv4.conf.all.forwarding=1  >> /etc/sysctl.conf
              echo net.ipv4.ip_forward=1 >> /etc/sysctl.conf
              echo net.ipv4.conf.all.rp_filter=0 >> /etc/sysctl.conf
              systemctl restart network
              systemctl enable zebra
              systemctl start zebra
              systemctl enable ospfd
              systemctl start ospfd
              SHELL
          when "R2"
            box.vm.provision "shell", run: "always", inline: <<-SHELL
              setenforce 0
              yum install -y quagga
              cp /vagrant/network-scripts/ifcfg-vlan12-r2 /etc/sysconfig/network-scripts/ifcfg-vlan12
              cp /vagrant/network-scripts/ifcfg-vlan23-r2 /etc/sysconfig/network-scripts/ifcfg-vlan23
              cp /vagrant/network-scripts/daemons /etc/quagga/daemons
              cp /vagrant/network-scripts/r2-zebra.conf /etc/quagga/zebra.conf
              cp /vagrant/network-scripts/r2-ospfd.conf /etc/quagga/ospfd.conf
              chown quagga:quaggavt /etc/quagga/ospfd.conf
              chown quagga:quagga /etc/quagga/zebra.conf              
              echo net.ipv4.conf.all.forwarding=1  >> /etc/sysctl.conf
              echo net.ipv4.ip_forward=1 >> /etc/sysctl.conf
              echo net.ipv4.conf.all.rp_filter=0 >> /etc/sysctl.conf
              systemctl restart network
              systemctl enable zebra
              systemctl start zebra
              systemctl enable ospfd
              systemctl start ospfd
              SHELL
          when "R3"
            box.vm.provision "shell", run: "always", inline: <<-SHELL
              setenforce 0
              yum install -y quagga
              cp /vagrant/network-scripts/ifcfg-vlan13-r3 /etc/sysconfig/network-scripts/ifcfg-vlan13
              cp /vagrant/network-scripts/ifcfg-vlan23-r3 /etc/sysconfig/network-scripts/ifcfg-vlan23
              cp /vagrant/network-scripts/daemons /etc/quagga/daemons
              cp /vagrant/network-scripts/r3-zebra.conf /etc/quagga/zebra.conf
              cp /vagrant/network-scripts/r3-ospfd.conf /etc/quagga/ospfd.conf
              chown quagga:quaggavt /etc/quagga/ospfd.conf
              chown quagga:quagga /etc/quagga/zebra.conf
              echo net.ipv4.conf.all.forwarding=1  >> /etc/sysctl.conf
              echo net.ipv4.ip_forward=1 >> /etc/sysctl.conf
              echo net.ipv4.conf.all.rp_filter=0 >> /etc/sysctl.conf
              systemctl restart network
              systemctl enable zebra
              systemctl start zebra
              systemctl enable ospfd
              systemctl start ospfd
              SHELL

        end

      end

  end
  
  
end
