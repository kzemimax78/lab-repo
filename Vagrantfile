# -*- mode: ruby -*-
# vi: set ft=ruby :

nodes = {
    "k8s-lb" => { ip: "192.168.56.10", mem: 2048, cpus: 2, port_offset: 0, role: "lb" },
    "k8s-ctrpln-1" => { ip: "192.168.56.10", mem: 2048, cpus: 2, port_offset: 1, role: "ctrpl" },
    "k8s-ctrpln-2" => { ip: "192.168.56.11", mem: 2048, cpus: 2, port_offset: 2, role: "ctrpl" },
    "k8s-worker-1" => { ip: "192.168.56.101", mem: 4096, cpus: 2, port_offset: 4, role: "worker" },
    "k8s-worker-2" => { ip: "192.168.56.102", mem: 4096, cpus: 2, port_offset: 6, role: "worker" },
    "k8s-worker-3" => { ip: "192.168.56.103", mem: 4096, cpus: 2, port_offset: 8, role: "worker" }
  }

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-24.04"
  nodes.each do |name, opts|
    config.vm.define name do |node_config|
      node_config.vm.hostname = name
      node_config.vm.network "private_network", ip: opts[:ip], netmask: "255.255.255.0" 
      node_config.vm.network "forwarded_port", guest: 22, host: 2720 + opts[:port_offset]

      node_config.vm.provider "virtualbox" do |vb|
        vb.memory = opts[:mem]
        vb.cpus = opts[:cpus]
        vb.name = name
      end
    end
  end
end
