Vagrant.configure("2") do |config|
  config.ssh.insert_key = false

  config.vm.define "ansible" do |ansible|
    ansible.vm.box = "bento/ubuntu-16.04"
    ansible.vm.synced_folder "playbook", "/home/vagrant/playbook"
    ansible.vm.hostname = "ansible"
    ansible.vm.network "private_network", virtualbox__intnet: "demo", ip: "192.168.0.2"
    ansible.vm.provision "shell", inline: <<~SHELL
      apt-add-repository -y ppa:ansible/ansible
      apt-get update -y
      apt-get install -y ansible
      echo '192.168.0.3 workstation' >> /etc/hosts
      ssh-keyscan workstation >> /home/vagrant/.ssh/known_hosts
      chown -R vagrant:vagrant /home/vagrant/.ssh
    SHELL
    ansible.vm.provision "file", source: "~/.vagrant.d/insecure_private_key", destination: "/home/vagrant/.ssh/id_rsa"
  end

  config.vm.define "workstation" do |workstation|
    workstation.vm.box = "bento/ubuntu-16.04"
    workstation.vm.hostname = "workstation"
    workstation.vm.network "private_network", virtualbox__intnet: "demo", ip: "192.168.0.3"
    workstation.vm.provision "shell", inline: <<~SHELL
      echo '192.168.0.2 ansible' >> /etc/hosts
    SHELL
  end
end
