## Установка CH:

sudo apt-get install -y apt-transport-https ca-certificates dirmngr
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 8919F6BD2B48D754

echo "deb https://packages.clickhouse.com/deb stable main" | sudo tee \
    /etc/apt/sources.list.d/clickhouse.list
sudo apt-get update

sudo apt-get install -y clickhouse-server clickhouse-client

sudo service clickhouse-server start
clickhouse-client # or "clickhouse-client --password" if you've set up a password.

### Добавление пользователя:

cat /etc/clickhouse-server/users.xml

<yandex>
....
    <users>
        <ch_user>
            <password>ch_password</password>
            <access_management>0</access_management>
            <networks incl="networks" replace="replace">
                <ip>127.0.0.1</ip>
            </networks>
        </ch_user>
    </users>
....
</yandex>


## Настрйка профиля:


cat /etc/clickhouse-server/users.xml
<yandex>
....
    </profiles>
        <ronly>
            <readonly>1</readonly>
            <max_execution_time>180</max_execution_time>
        </ronly>
    </profiles>
....
....
    <users>
        <ch_user>
            <profile>ronly</profile>
            <password>ch_password</password>
            <access_management>0</access_management>
            <networks incl="networks" replace="replace">
                <ip>127.0.0.1</ip>
            </networks>
        </ch_user>
    </users>
</yandex>

## Настройка SSL:

certbot.eff.org

or

openssl req -subj "/CN=localhost" -new -newkey rsa:2048 -days 365 -nodes -x509 -keyout /etc/clickhouse-server/server.key -out /etc/clickhouse-server/server.crt



openssl dhparam -out /etc/clickhouse-server/dhparam.pem 4096


cd /etc/clickhouse-server

sudo chown clickhouse:clickhouse server.crt
sudo chown clickhouse:clickhouse server.key
sudo chown clickhouse:clickhouse dhparam.pem


/etc/clickhouse-server/config.xml
<yandex>
    <https_port>8443</https_port>
    <tcp_port_secure>9440</tcp_port_secure>
    <!--
    <http_port>8123</http_port>
    <tcp_port>9000</tcp_port>
    -->
</yandex>



<yandex>
  <openSSL>
    <server>
      <certificateFile>/etc/clickhouse-server/server.crt</certificateFile
      <privateKeyFile>/etc/clickhouse-server/server.key</privateKeyFile>
      <dhParamsFile>/etc/clickhouse-server/dhparam.pem</dhParamsFile>
      <verificationMode>none</verificationMode>
      <loadDefaultCAFile>true</loadDefaultCAFile>
      <cacheSessions>false</cacheSessions> 
      <disableProtocols>sslv2,sslv3</disableProtocols> 
      <preferServerCiphers>true</preferServerCiphers>
    </server>
  </openSSL>
</yandex>






/etc/clickhouse-client/config.xml
<verificationMode>none</verificationMode>

## Настройка квот:

cat /etc/clickhouse-server/users.xml

<yandex>
....
    <quotas>
        <user>
            <interval>
                <duration>3600</duration>
                <queries>100</queries>
                <errors>0</errors>
                <result_rows>0</result_rows>
                <read_rows>10000000</read_rows>
                <execution_time>0</execution_time>
            </interval>
        </user>
    </quotas>
</yandex>

## Шаридирование:

Данные действия необходимо производить на двух нодах

vim /etc/clickhouse-server/config.xml

    <remote_servers incl="clickhouse_remote_servers">
    </remote_servers>
    <include_from>/etc/clickhouse-server/cluster.xml</include_from>



vim /etc/clickhouse-server/cluster.xml

<?xml version="1.0"?>
<yandex>
    <clickhouse_remote_servers>
        <local> // Название кластера
            <shard>
                <replica>
                    <host>167.99.142.32</host> // первая нода в нашем кластере
                    <port>9000</port>
                </replica>
						</shard>
						<shard>
                <replica>
                    <host>159.65.123.161</host> // вторая нода в нашем кластере
                    <port>9000</port>
                </replica>
            </shard>
        </local>
    </clickhouse_remote_servers>
</yandex>


vim /etc/clickhouse-server/config.xml

<listen_host>0.0.0.0</listen_host>


sudo chown clickhouse:clickhouse /etc/clickhouse-server/cluster.xml
service clickhouse-server status



CREATE TABLE ch_local
(
    id Int64,
    title String,
    description String,
    content String,
    date Date
)
ENGINE = MergeTree()
PARTITION BY date
ORDER BY id;


CREATE TABLE ch_distributed
(
    id Int64,
    title String,
    description String,
    content String,
    date Date
)
ENGINE = Distributed('local', 'default', 'ch_local', rand());



#  clickhouse-client --query "INSERT INTO ch_distributed FORMAT CSV" < ch_distributed.csv

clickhouse-client
INSERT INTO ch_distributed (id, title, description, content, date) VALUES(1, 'title', 'desc', 'content', '2018-07-03')


SELECT count(*)
FROM ch_distributed

Query id: 1611236f-d12b-4b24-9ac9-44f854232d3a7

┌─count()─┐
│      10 │
└─────────┘

1 rows in set. Elapsed: 0.013 sec. 
