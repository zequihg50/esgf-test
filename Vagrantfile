# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.define :di do |di|
    di.vm.box = "centos/6"
    di.vm.hostname = "esgf.test.es"

    di.vm.provision "file", source: "~/.vagrant.d/insecure_private_key", destination: "/tmp/id_rsa"
    di.vm.provision "shell", inline: "sudo bash -c 'mkdir /root/.ssh && ssh-keygen -y -f /tmp/id_rsa > /root/.ssh/authorized_keys && chmod 700 /root/.ssh && chmod 600 /root/.ssh/authorized_keys && sed -i \'s/#PermitRootLogin/PermitRootLogin/\' /etc/ssh/sshd_config && cp /tmp/id_rsa /root/.ssh/id_rsa' ; yum install -y git"
  end

  config.vm.provision "shell", inline: "sudo yum install -y expect libselinux-python"

  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
    v.cpus = 2
  end
end
