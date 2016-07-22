# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
vagrant_root = File.dirname(__FILE__)

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "bento/ubuntu-16.04"
  #config.vm.box = "ubuntu/xenial64"
  #config.vm.box = "ubuntu/trusty64"
  config.vm.provider "virtualbox" do |v|
    v.memory = 6144
    v.cpus = 2
  end

  #if File.directory?(File.expand_path("~/projects")) 
  #  config.vm.synced_folder "~/projects", "/home/vagrant/projects"
  #end

	host_name = "ros2"
	config.vm.define "machine1" do |machine|
		if Vagrant.has_plugin?("vagrant-timezone")
			config.timezone.value = :host
		end 
		machine.vm.hostname = host_name
		# Only execute once the Ansible provisioner,
		# when all the machines are up and ready.
		machine.vm.provision :ansible do |ansible|
			# Disable default limit to connect to all the machines
			ansible.limit = "machine1"
			ansible.playbook = "main.yaml"
			ansible.extra_vars = { 
				host_name: host_name,
			}
		end
	end
end
