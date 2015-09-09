# Provisioning Script
$script = <<SCRIPT
echo "Updating package index..."
apt-get update
source /etc/lsb-release && echo "deb http://download.rethinkdb.com/apt $DISTRIB_CODENAME main" | sudo tee /etc/apt/sources.list.d/rethinkdb.list
wget -qO- http://download.rethinkdb.com/apt/pubkey.gpg | sudo apt-key add -
apt-get install software-properties-common python-software-properties git python3-pip python3-dev screen -y
sudo add-apt-repository ppa:chris-lea/redis-server
apt-get update
echo "Installing RethinkDB..."
apt-get install rethinkdb -y
cp /home/vagrant/shared/instance1.conf /etc/rethinkdb/instances.d/instance1.conf
/etc/init.d/rethinkdb restart
echo "RethinkDB installation complete, installing Redis..."
apt-get install redis-server -y
cp /home/vagrant/shared/redis.conf /etc/redis/redis.conf
service redis-server restart
echo "Redis installation complete, cloning PyWebhooks..."
su vagrant
git clone https://github.com/chadlung/pywebhooks
cd pywebhooks
pip3 install --upgrade -r requirements.txt
SCRIPT

Vagrant.configure(2) do |config|
  config.vm.box = "dhoppe/ubuntu-14.04.2-amd64-nocm"
  config.vm.provision "shell", inline: $script, privileged: true
  config.vm.synced_folder "./shared", "/home/vagrant/shared"
  config.vm.hostname = "pywebhooks-dev"
  config.vm.network "forwarded_port", guest: 8080, host: 8080, auto_correct: true
  config.vm.network "forwarded_port", guest: 28015, host: 28015
  config.vm.network "forwarded_port", guest: 29015, host: 29015

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
  end
end
