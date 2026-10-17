# -*- mode: ruby -*-
# vi: set ft=ruby :

# Define the shell commands used to install the required dependencies.
install_deps = <<-SHELL

# Update the package lists.
	apt-get update
# Install Java Development Kit (JDK) version 17.
	apt-get install -y openjdk-17-jdk
SHELL

Vagrant.configure("2") do |config|

  # Specify the Ubuntu 24.04 virtual machine image.
  config.vm.box = "bento/ubuntu-24.04"

  # Specify the version of the virtual machine image.
  config.vm.box_version = "202510.26.0"

  
  # Assign a private IP address to the virtual machine.
  config.vm.network "private_network", ip: "192.168.100.100"

  # Configure the VirtualBox virtual machine resources.  
  config.vm.provider "virtualbox" do |vb|
     
  # Allocate 4096 MB of RAM.
	vb.memory = "4096"

  # Allocate 2 virtual CPUs.
	vb.cpus = 2	
   end

  # Install the required dependencies when provisioning the VM
  config.vm.provision "shell", inline: install_deps

  # Run the following trigger after the VM starts with `vagrant up`.
  config.trigger.after :up do |trigger|
     # Set the trigger name displayed in the Vagrant output.
     trigger.name = "Start gradlew"

     # Display an informational message when the trigger runs.
     trigger.info = "Starting the application..."

     # Execute the application startup command inside the VM.
     trigger.run_remote = {
	inline: "cd /vagrant && nohup ./gradlew bootRun > /tmp/bootRun.log 2>&1 < /dev/null &"
     }
  end
end