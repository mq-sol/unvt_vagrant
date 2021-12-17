# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
  end

  vm_name = "unvt-dev"

  config.vm.box = "ubuntu/focal64"
  config.vm.hostname = 'unvt-dev'
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 443, host: 443
  config.vm.network "private_network", ip: "192.168.56.50"
 
  config.vm.provision "shell", inline: <<-SHELL
    # ssh
    sudo sed -i -e 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config
    sudo systemctl restart sshd.service
    sudo sh -c “echo -e ‘nameserver 8.8.8.8\nnameserver 8.8.4.4’ >> /etc/resolv.conf”

    # apt update
    sudo apt update -y
    sudo apt upgrade -y

    # 必要なパッケージのインストール
    ## Docker
    sudo apt -y remove docker docker-engine docker.io containerd runc
    sudo apt -y install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    sudo apt -y update
    sudo apt -y install docker-ce docker-ce-cli containerd.io
    sudo usermod -aG docker vagrant
    sudo systemctl restart docker

    ## ruby
    sudo apt install -y g++ gcc autoconf automake bison libc6-dev libffi-dev libgdbm-dev libncurses5-dev libsqlite3-dev libtool libyaml-dev make pkg-config sqlite3 zlib1g-dev libgmp-dev libreadline-dev libssl-dev
    sudo apt install -y libreadline-dev
    sudo apt install -y ruby-full

    ## tippecanoe
    git clone https://github.com/mapbox/tippecanoe.git
    cd tippecanoe
    make -j
    sudo make install

    ## pdal
    cd
    wget https://repo.anaconda.com/miniconda/Miniconda3-py38_4.10.3-Linux-x86_64.sh
    bash Miniconda3-py38_4.10.3-Linux-x86_64.sh -b -p /home/vagrant/miniconda3
    /home/vagrant/miniconda3/conda create --name pdalworkshop
    /home/vagrant/miniconda3/conda activate pdalworkshop
    /home/vagrant/miniconda3/conda install -c conda-forge pdal python-pdal gdal entwine matplotlib

    # 必要なものをGit から取得する
    git clone https://github.com/optgeo/kid-c
    git clone https://github.com/optgeo/cudi

  SHELL
end
