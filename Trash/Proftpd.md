Устанавливаем:

# apt-get update && apt-get upgrade
# apt-get install proftpd-basic
 - Команды для работы с демоном /etc/init.d/proftpd;
{start|status|force-start|stop|force-stop|reload|restart|force-reload|check-config}
 - Проверка конфигурационного файла;
# proftpd -t,--configtest
 - Показать статистику использования;
# ftpwho или ftptop

Подготавливаем конфигурационный файл:

# cp /etc/proftpd/proftpd.conf /etc/proftpd/proftpd.conf.old
# nano /etc/proftpd/proftpd.conf
UseIPv6                         off
ServerName                      "Debian"
ServerType                      standalone
DefaultRoot                     /home/proftpd/
RequireValidShell               off
Port                            21
MaxInstances                    30
User                            proftpd
Group                           nogroup
Umask                           022  022 # Присваиваемые права при создании -  файла | каталога;
AllowOverwrite                  on
# AuthOrder                     mod_auth_pam.c* mod_auth_unix.c
AuthUserFile                    /etc/proftpd/users.passwd
Include /etc/proftpd/tls.conf
Include /etc/proftpd/conf.d/

Шифрование TLS:

 - Генерируем сертефикаты;
# openssl req -x509 -newkey rsa:2048 -keyout /etc/ssl/private/proftpd.key -out /etc/ssl/certs/proftpd.crt -nodes -days 365
# openssl dhparam -out /etc/proftpd/CA.pem 2048 или 4096
 - Настраиваем права;
# chmod 0600 /etc/ssl/private/proftpd.key
# chmod 0640 /etc/ssl/certs/proftpd.crt
 - Подключаем модуль;
# nano /etc/proftpd/modules.conf
LoadModule mod_tls.c
 - Редактируем конфиг;
# nano /etc/proftpd/tls.conf
TLSEngine                               on
TLSLog                                  /var/log/proftpd/tls.log
TLSProtocol                             SSLv23
TLSRSACertificateFile                   /etc/ssl/certs/proftpd.crt
TLSRSACertificateKeyFile                /etc/ssl/private/proftpd.key
#TLSCACertificateFile                    /etc/proftpd/dhparams.pem
TLSOptions				AllowClientRenegotiations
TLSVerifyClient                         off
TLSRequired                             on # Если off, то возможность одновременного использования TLS и noTLS;

Добавляем пользователей:
От имени которых, будут работать виртуальные пользователи.

 -b Начальная часть пути нового домашнего каталога пользователя. Имя пользователя будет добавлено в конец домашнего каталога;
 -m Создать домашний каталог пользователя;
 -U Создать группу с тем же именем что и у пользователя, и добавить пользователя в эту группу;
 -s Имя регистрационной оболочки пользователя;
# mkdir /home/proftpd && chown proftpd:nogroup /home/proftpd
# useradd entity0 -b /home/proftpd/ -m -U -s /bin/false && passwd entity0 # Pass
# useradd entity1 -b /home/proftpd/ -m -U -s /bin/false && passwd entity1 # Pass
# useradd entity2 -b /home/proftpd/ -m -U -s /bin/false && passwd entity2 # Pass

# useradd entity2 -b /home/proftpd/ -m -U -s /bin/false && passwd entity2

 - Удалить пользователя;
# userdel -r username
 - Узнать uid= и gid= пользователя;
# id username

страиваем авторизацию для виртуальных пользователей.

Показать листинг: >
 - Добавить пользователя;
# ftpasswd --passwd --file=/etc/proftpd/users.passwd --name=test --uid=1001 --gid=1001 --home=/home/proftpd/ --shell=/bin/false
# ftpasswd --group --name=nogroup --file=/etc/proftpd/users.group --gid=1001 --member test
 - Заблокировать, разблокировать пользователя. Символ ! вначале;
# ftpasswd --passwd --file=/etc/proftpd/users.passwd --name=test --lock
# ftpasswd --passwd --file=/etc/proftpd/users.passwd --name=test --unlock
 - Изменить пользовательский пароль;
# ftpasswd --passwd --file=/etc/proftpd/users.passwd --name=test --change-password
 - Удалить пользователя;
# ftpasswd --passwd --file=/etc/proftpd/users.passwd --name=test --delete-user
 - Настраиваем entity[0-2];
entity0: pass - *******
# ftpasswd --passwd --file=/etc/proftpd/users.passwd --name=entity0_user1 --uid=1001 --gid=1001 --home=/home/proftpd/entity0/user1 --shell=/bin/false

entity1: pass - *******
# ftpasswd --passwd --file=/etc/proftpd/users.passwd --name=entity1_user1 --uid=1002 --gid=1002 --home=/home/proftpd/entity1/user1 --shell=/bin/false

entity2: pass - *******
# ftpasswd --passwd --file=/etc/proftpd/users.passwd --name=entity2_user1 --uid=1003 --gid=1003 --home=/home/proftpd/entity2/user1 --shell=/bin/false
 - Выставляем рекурсивно права на директории;
# cd /home/proftpd
# find . -type d -exec chmod 0755 {} \;

Virtual user settings:
Настройка доступа виртуальных пользователей к директориям. + скрытые файлы.

Показать листинг: >
# nano /etc/proftpd/conf.d/directory.conf
# HIDE
<Directory /home/proftpd/>
HideFiles ^\.
#HideFiles ^\.(bash_logout|bashrc|profile)$
#PathDenyFilter ^\.(bash_logout|bashrc|profile)$
</Directory>

# ENITY0
<Directory /home/proftpd/entity0/user1>
    <Limit ALL>
        Order deny,allow
        AllowUser entity0_user1,entity1_user1
    </Limit>
</Directory>

<Directory /home/proftpd/entity0/user2>
    <Limit ALL>
        Order deny,allow
        AllowUser entity0_user2
    </Limit>
</Directory>

<Directory /home/proftpd/entity0/user3>
    <Limit ALL>
        Order deny,allow
        AllowUser entity0_user3
    </Limit>
</Directory>

# ENITY1
<Directory /home/proftpd/entity1/user1>
    <Limit ALL>
        Order deny,allow
        AllowUser entity1_user1
    </Limit>
</Directory>

<Directory /home/proftpd/entity1/user2>
    <Limit ALL>
        Order deny,allow
        AllowUser entity1_user2
    </Limit>
</Directory>

<Directory /home/proftpd/entity1/user3>
    <Limit ALL>
        Order deny,allow
        AllowUser entity1_user3
    </Limit>
</Directory>

# ENITY2
<Directory /home/proftpd/entity2/user1>
    <Limit ALL>
        Order deny,allow
        AllowUser entity2_user1
    </Limit>
</Directory>

<Directory /home/proftpd/entity2/user2>
    <Limit ALL>
        Order deny,allow
        AllowUser entity2_user2
    </Limit>
</Directory>

<Directory /home/proftpd/entity2/user3>
    <Limit ALL>
        Order deny,allow
        AllowUser entity2_user3
    </Limit>
</Directory>
Список команд FTP: [Link]

READ - все FTP-команды, связанные с чтением файлов (за исключением команд выдачи листинга содержимого директории), (RETR, SITE, SIZE, STAT);
WRITE - все FTP-команды, связанные с созданием, записью или удалением файлов или директорий (APPE, DELE, MKD, RMD, RNTO, STOR, XMKD, XRMD);
DIRS — все FTP-команды, связанные с выдачей листинга содержимого директории (CDUP, CWD, LIST, MDTM, NLST, PWD, RNFR, XCUP, XCWD, XPWD);
ALL - все FTP-команды (включает в себя все три класса READ, WRITE и DIRS).


ftpasswd --passwd --file=/etc/proftpd/ftpd.passwd --name=apkinformer_com --uid=33 --gid=33 --home=/var/tmp --shell=/usr/sbin/nologin