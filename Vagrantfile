# -*- mode: ruby -*-
# # vi: set ft=ruby :
Vagrant.configure(2) do |config|
  config.vm.define "Kubernetes5" do |s|
    s.ssh.forward_agent = true
    s.vm.box = "ubuntu/xenial64"
    s.vm.hostname = "Kubernetes5"
    s.vm.provision :shell, inline: "sudo apt-get update && apt-get install -y apt-transport-https"
    s.vm.provision :shell, inline: "sudo apt install -y docker.io"
    s.vm.provision :shell, inline: "sudo systemctl enable docker"
    s.vm.provision :shell, inline: "sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add "
    s.vm.provision :shell, inline: "sudo apt-add-repository 'deb http://apt.kubernetes.io/ kubernetes-xenial main' "
    s.vm.provision :shell, inline: "apt-get update -y"
    s.vm.provision :shell, inline: "apt-get install -y kubelet kubeadm kubectl kubernetes-cni"
    s.vm.provision :shell, inline: "sudo swapoff -a"
    s.vm.provision :shell, inline: "wget https://github.com/kubernetes/kops/releases/download/1.10.0/kops-linux-amd64"
    s.vm.provision :shell, inline: "sudo chmod +x kops-linux-amd64"
    s.vm.provision :shell, inline: "sudo mv kops-linux-amd64 /usr/local/bin/kops"


    s.vm.network "private_network", ip: "192.168.56.20", netmask: "255.255.255.0",
      auto_config: true,
      virtualbox__intnet: "services"
    config.vm.network "public_network", type: "dhcp", bridge: "eth0"
    s.vm.provider "virtualbox" do |v|
      v.name = "Kubernetes5"
      v.memory = 2048
      v.gui = false
    end
  end
end
