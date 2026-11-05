Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"
  config.vm.hostname = "k3s-dev"

  # Увеличаваме времето за изчакване на 6 минути
  config.vm.boot_timeout = 360

  # Оставяме само Port Forwarding (махли private_network за момента)
  config.vm.network "forwarded_port", guest: 30080, host: 30080
  config.vm.network "forwarded_port", guest: 8080, host: 8080

  config.vm.provider "virtualbox" do |v|
    v.memory = 3072
    v.cpus = 2
  end

  config.vm.provision "shell", inline: <<-SHELL
    curl -sfL https://get.k3s.io | sh -
    sudo chmod 644 /etc/rancher/k3s/k3s.yaml
    echo "export KUBECONFIG=/etc/rancher/k3s/k3s.yaml" >> /home/vagrant/.bashrc
  SHELL
end