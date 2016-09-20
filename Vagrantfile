# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
vagrant_root = File.dirname(__FILE__)
hostname = "ros2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "bento/ubuntu-16.04"
  config.vm.hostname = hostname
  config.vm.provider "virtualbox" do |v|
    v.name = hostname
    v.memory = 6144
    v.cpus = 2
  end

  # link to projects folder
  if File.directory?(File.expand_path("~/projects")) 
    config.vm.synced_folder "~/projects", "/home/vagrant/projects"
  end

	config.vm.define "machine1" do |machine|
		if Vagrant.has_plugin?("vagrant-timezone")
			config.timezone.value = :host
		end 
		# Only execute once the Ansible provisioner,
		# when all the machines are up and ready.
		machine.vm.provision :ansible do |ansible|
			# Disable default limit to connect to all the machines
			ansible.limit = "machine1"
			ansible.playbook = "main.yaml"
			ansible.extra_vars = { 
				host_name: hostname,
			}
		end
	end
end
