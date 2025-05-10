# Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"

  # Server VM
  config.vm.define "server" do |server|
    server.vm.hostname = "server.loc"
    server.vm.network "private_network", ip: "192.168.56.10"
    server.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.cpus = 2
    end
    # Copy Ansible files to server
    server.vm.provision "file", source: "ansible/server", destination: "/home/vagrant/ansible"
    # Install Ansible and run playbook locally
    server.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update
      sudo apt-get install -y ansible
      ansible-playbook /home/vagrant/ansible/playbook.yml
    SHELL
  end

  # Client VM
  config.vm.define "client" do |client|
    client.vm.hostname = "client.loc"
    client.vm.network "private_network", ip: "192.168.56.20"
    client.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.cpus = 2
    end
    # Copy Ansible files to client
    client.vm.provision "file", source: "ansible/client", destination: "/home/vagrant/ansible"
    # Install Ansible and run playbook locally
    client.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update
      sudo apt-get install -y ansible
      ansible-playbook /home/vagrant/ansible/playbook.yml
    SHELL
  end
end