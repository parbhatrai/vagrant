# -*- mode: ruby -*-
# vi: set ft=ruby :
require "yaml"
guests = YAML.load_file("machines.yaml")

Vagrant.configure("2") do |config|
  guests.each do |guest_vm|
    config.vm.define guest_vm['name'] do |vm|
      set_hostname(guest_vm, vm)
      set_box(guest_vm, vm)
      set_cpus_and_memory(guest_vm, vm)
      set_private_ip(guest_vm, vm)
      set_run_install_scripts(guest_vm, vm)
    end
  end
end

def set_hostname(guest_vm, vm)
  vm.vm.hostname = guest_vm["name"]
end

def set_box(guest_vm, vm)
  vm.vm.box = guest_vm["box"]
end

def set_cpus_and_memory(guest_vm, vm)
  vm.vm.provider "virtualbox" do |vb|
    vb.cpus = guest_vm["cpus"]
    vb.memory = guest_vm["memory"]
  end
end

def set_private_ip(guest_vm, vm)
  vm.vm.network "private_network", ip: guest_vm["private_ip"]
end

def set_run_install_scripts(guest_vm, vm)
  guest_vm["scripts"].each do |script|
    vm.vm.provision "shell", path: script
  end
end