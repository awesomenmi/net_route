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
          	
        case boxname.to_s
        when "R1"
          box.vm.provision "shell", inline: <<-SHELL
            iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
            echo 1 > /proc/sys/net/ipv4/ip_forward
          SHELL
        end
      end
  end

  config.vm.provision "ansible" do |ansible|
  	ansible.playbook = "provision.yml"
	ansible.verbose = "vv"
  end
end
