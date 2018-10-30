Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.network "public_network", bridge: "Intel(R) Ethernet Connection I217-LM"

  config.vm.synced_folder "../warehouse", "/warehouse"

  config.vm.provision "shell", 
  inline: <<-SHELL
	sudo su
	apt-get update

    add-apt-repository -y ppa:webupd8team/java
    apt-get update
    apt-get -y upgrade
    echo debconf shared/accepted-oracle-license-v1-1 select true | sudo debconf-set-selections
    echo debconf shared/accepted-oracle-license-v1-1 seen true | sudo debconf-set-selections
    sudo apt-get -y --force-yes install oracle-java8-installer

    apt-get install -y python-pip
    apt-get install -y dateutil
    pip install boto3

    apt-get install -y --force-yes zip

    apt-get install -y --force-yes awscli

    mkdir /spark
    cd /spark/
    wget -q http://mirrors.wuchna.com/apachemirror/spark/spark-2.3.2/spark-2.3.2-bin-hadoop2.7.tgz
    tar xzvf spark-2.3.2-bin-hadoop2.7.tgz

    export PATH=/spark/spark-2.3.2-bin-hadoop2.7/bin/:$PATH

   SHELL
end
