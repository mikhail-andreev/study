# FIREWALL:
```bash


sudo ufw app list #- выдает спискок приложений, которые "стучаться" в сеть

sudo ufw status #- выдает список и покзаывет статуст каждого приложения

sudo ufw allow 'app_name' #- разрешает выбранному приложению доступ к сети

# УПРАВЛЕНИЕ ПРИЛОЖЕНИЯМИ:

sudo systemctl status app_name #- выдает статус выбранного приложения

sudo systemctl restart app_name #- презапуксает выбранное приложение

sudo systemctl enable\disable app_name #- выключение/выклбчение выбранного сервиса
```

NGINX

sudo chown -R $USER:$USER /var/www/your_domain/html - назначение владения дирркторией, нужно для того чтобы была возможность чтения/записи

sudo chmod -R 755 /var/www/site.ru - установка прав доступа

sudo vim /etc/nginx/sites-available/your_domain - создание файла с директивами для запуска сервера

sudo ln -s /etc/nginx/sites-available/your_domain /etc/nginx/sites-enabled/ - создание файловой ссылки на диррективы, чтобы nginx подтянул их при запуске

sudo nginx -t - проверка синтаскиса конфигурационных файлов nginx

sudo nginx -s reload - мягкая перезагрузка Nginx

Test pull

MYSQL

mysql -u root -p -вход в мускл когда включена аутентификация root с помощью пароля

sudo mysql_secure_installation - запускает скрипт настройки безопасности

mysqldump -u root -p db_name > /db_backup.sql

SELECT user,authentication_string,plugin,host FROM mysql.user;

FLUSH PRIVILEGES; - перезагрузка прав доступа пользователей

CREATE USER 'miha'@'localhost' IDENTIFIED BY 'password'; - создать пользователя
 
GRANT ALL PRIVILEGES ON *.* TO 'miha'@'localhost' WITH GRANT OPTION; - дать все права
Ansible 



CREATE USER 'viktor_samohvalov' IDENTIFIED BY 'cxPQrgwA6X4PFUDyvFbz'; - создать пользователя
 
GRANT ALL PRIVILEGES ON *.* TO 'miha'@'localhost' WITH GRANT OPTION; - дать все права
GRANT SELECT, VIEW SHOW PRIVILEGES ON *.* TO 'viktor_samohvalov'@'localhost' WITH GRANT OPTION; - дать все права
Ansible 

 GRANT SELECT ON 'rtb'.* TO 'viktor_samohvalov'@'%' IDENTIFIED BY 'password123321'; FLUSH PRIVILEGES;
 GRANT SELECT ON 'rtb'.* TO 'viktor_samohvalov'@'%'; 

ansible-inventory --list -y - воводит список подключенных серверов

ansible all -m ping -u root - тестирование подключения к серверам, вместо root - имя пользователя

ansible all -a "df -h" -u root - проверка использования дисков на всех подключенных серверах

CAT /PROC/

cat /etc/passwd
cat /proc/loadavg
cat /proc/cpuinfo
cat /proc/interrupts
cat /proc/partitions
cat /proc/PID/status
cat /proc/uptime
cat /proc/meminfo

LSOF

lsof -i 4 -a -p 1234 (просмотр всех соединений IPv4, открытых процессом с PID = 1234)
lsof -i tcp:80 (просмотр информации о процессе, который прослушивает 80 TCP порт)
lsof /dev/hd4 (Список открытых файлов на устройстве /dev/hd4)
lsof /dev/cdrom (Список процессов, работающих с CD ROM)
lsof -c ssh (Список подключений по ssh)

GITHUB

git checkout -b add/vasiliyshilov - создаст нам отдельную ветку + переключится в неё
git add . добавит в новый коммит все изменившиеся файлы в папке
git commit зафиксирует изменения
git push --set-upstream origin add/vasiliyshilov отправит изменения на гит сервер

SSH - туннели

ssh -N -L 6379:adsbid-stage-rs01-ovh:6379 adsbid-stage-rs01-ovh - redis 

ssh -N -L 3301:adsbid-stage-tnt01-ovh:3301 adsbid-stage-tnt01-ovh - тарантул


РАЗНОЕ
lshw -businfo - краткая инофрмация об установленномс железе

free -h - объем оперативки в удобном формате

df -h - информация о жестких дисках в удобном формате

curl -4 icanhazip.com - показывает ip-адресс машины с помощью стороннего сервиса

ls -l - список файлов с указанием владельцев

ssh-keygen -t rsa -b 4096 -генерация ключа ssh

ssh-copy-id user_name@ip-address - копировать ssh ключ на удаленную машину

