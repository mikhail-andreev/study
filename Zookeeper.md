### Установка:

sudo apt update
sudo apt install -y default-jre-headless
sudo mkdir -p /opt/zookeeper
sudo su -l
cd /opt/zookeeper
wget https://apache-mirror.rbc.ru/pub/apache/zookeeper/zookeeper-3.7.0/apache-zookeeper-3.7.0-bin.tar.gz
tar xzfv apache-zookeeper-3.7.0-bin.tar.gz
mv apache-zookeeper-3.7.0-bin/* ./
rm -rf apache-zookeeper-3.7.0-bin
rm apache-zookeeper-3.7.0-bin.tar.gz

### Конфигурация ZK:

vim conf/zoo.cfg

tickTime=2000
dataDir=/var/lib/zookeeper
clientPort=2181


./bin/zkServer.sh start
./bin/zkCli.sh -server localhost:2181
./bin/zkServer.sh stop

### Создание сервиса ZK

useradd -M zookeeper

chown -R zookeeper:zookeeper /opt/zookeeper
mkdir /var/lib/zookeeper
chown -R zookeeper:zookeeper /var/lib/zookeeper

vim /lib/systemd/system/zookeeper.service

### Содержимое zookeeper.service:

[Unit]
Description=zookeeper:3.7.0
After=network.target

[Service]
Type=forking
User=zookeeper
Group=zookeeper

WorkingDirectory=/opt/zookeeper

ExecStart=/opt/zookeeper/bin/zkServer.sh start
ExecStop=/opt/zookeeper/bin/zkServer.sh stop
ExecReload=/opt/zookeeper/bin/zkServer.sh restart

RestartSec=30
Restart=always

PrivateTmp=yes
PrivateDevices=yes

LimitCORE=infinity
LimitNOFILE=500000

[Install]
WantedBy=multi-user.target
Alias=zookeeper.service




service zookeeper start


