# FIREWALL:

sudo ufw app list #- выдает спискок приложений, которые "стучаться" в сеть

sudo ufw status #- выдает список и покзаывет статуст каждого приложения

sudo ufw allow 'app_name' #- разрешает выбранному приложению доступ к сети

# УПРАВЛЕНИЕ ПРИЛОЖЕНИЯМИ:

sudo systemctl status app_name #- выдает статус выбранного приложения

sudo systemctl restart app_name #- презапуксает выбранное приложение

sudo systemctl enable\disable app_name #- выключение/выклбчение выбранного сервиса
```

 
# ANSIBLE:
 

ansible-inventory --list -y - воводит список подключенных серверов

ansible all -m ping -u root - тестирование подключения к серверам, вместо root - имя пользователя

ansible all -a "df -h" -u root - проверка использования дисков на всех подключенных серверах

ansible-playbook --check --diff --private-key=~/.ssh/andreev-2-test zzz_test.yml

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

GRANT ALL PRIVILEGES ON 'bidnew_stage'.* TO 'psergeev'@'%' IDENTIFIED BY 'lR7bclzB6N'; FLUSH PRIVILEGES; 


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
