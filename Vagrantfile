# -*- mode: ruby -*-
# vi: set ft=ruby :

machines = {
  "node001"   => {"memory" => "1024", "cpu" => "1", "image" => "ubuntu/bionic64"},
  "node002"   => {"memory" => "1024", "cpu" => "1", "image" => "ubuntu/bionic64"},
  "node003"   => {"memory" => "1024", "cpu" => "1", "image" => "ubuntu/bionic64"},
  "node004"   => {"memory" => "1024", "cpu" => "1", "image" => "ubuntu/bionic64"}
}

Vagrant.configure("2") do |config|

  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "#{conf["image"]}"
      machine.vm.hostname = "#{name}"
      machine.vm.network "public_network"
      
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "#{name}"
        vb.memory = conf["memory"]
        vb.cpus = conf["cpu"]
        vb.customize ["modifyvm", :id, "--groups", "/Docker-SWARM"]
      
	  end
      machine.vm.provision "shell", path: "instalar-docker.sh"
      config.vm.provision :shell, :inline => "sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config; sudo systemctl restart sshd;", run: "always"
      
    end
  end
end