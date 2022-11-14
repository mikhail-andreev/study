## FIREWALL:

sudo ufw app list #- выдает спискок приложений, которые "стучаться" в сеть

sudo ufw status #- выдает список и покзаывет статуст каждого приложения

sudo ufw allow 'app_name' #- разрешает выбранному приложению доступ к сети

## УПРАВЛЕНИЕ ПРИЛОЖЕНИЯМИ:

sudo systemctl status app_name #- выдает статус выбранного приложения

sudo systemctl restart app_name #- презапуксает выбранное приложение

sudo systemctl enable\disable app_name #- выключение/выклбчение выбранного сервиса

## Инфо о системе

ncdu -x - посмотреть чем занят диск, без подмонтированых дисков
netstat -ltupan   - открытые порты

## Управление пользователями

sudo usermod -aG sudo user - дать права root существующему пользователю

### CAT /PROC/

cat /etc/passwd
cat /proc/loadavg
cat /proc/cpuinfo
cat /proc/interrupts
cat /proc/partitions
cat /proc/PID/status
cat /proc/uptime
cat /proc/meminfo


### LSOF

lsof -i 4 -a -p 1234 (просмотр всех соединений IPv4, открытых процессом с PID = 1234)
lsof -i tcp:80 (просмотр информации о процессе, который прослушивает 80 TCP порт)
lsof /dev/hd4 (Список открытых файлов на устройстве /dev/hd4)
lsof /dev/cdrom (Список процессов, работающих с CD ROM)
lsof -c ssh (Список подключений по ssh)


## SSH 

ssh-keygen -t rsa -b 4096 -генерация ключа ssh

ssh-copy-id user_name@ip-address - копировать ssh ключ на удаленную машину


ssh -N -L [LOCAL_IP:]LOCAL_PORT:DESTINATION:DESTINATION_PORT [USER@]SSH_SERVER
Понадобятся такие параметры:

[LOCAL_IP:]LOCAL_PORT – IP-адрес и номер порта локального компьютера. Если локальный IP не указан, SSH-клиент привязывается к локальному хосту.

DESTINATION:DESTINATION_PORT – IP/имя хоста и порт машины назначения.

[USER@]SERVER_IP – Удаленный пользователь и IP-адрес сервера.

В качестве LOCAL_PORT вы можете использовать любой номер порта больше, чем 1024. Значения меньше 1024 являются привилегированными портами и могут использоваться только пользователем root. Если SSH-сервер прослушивает не 22-й порт, который стоит по умолчанию, используйте опцию -p [PORT_NUMBER].

Имя хоста назначения должно иметь разрешение с сервера SSH.


scp /home/test.txt root@123.123.123.123:/directory - перенос файла с локальной машины на удаленную

scp root@123.123.123.123:/home/test.txt /directory - перенос файла с удаленной машины на локальную

### SSH скопировать свой ключ

```cd ~;  mkdir .ssh ; chmod 700 .ssh && echo ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDN6esyjE2jKgg1q2C2ImpRT+ZPkjE9/FumPbjoykAhFWatAQwW718ODIg219CMjHPEUSPhHzxz9D5SA2sAXG5Ddv29t6bK4HDZcRBtuYglD3Tr80lLXYoMaMMJTlNLxf3uaAPsHxWjLVHiv/CPvjbQp5CUlXXzj8/nEERBg7K2KJz2DIsR5BDZT2vOfOL0ajdzCFvKEbJDU5Dy/IQDV0j2K3ylDdjwYN6ZlyotfgudyxekLh2JaCBY7sOh3nE5dlWb7cmx02+xB47npJrJxlUmq1klerBhp6zEVPTG7RZk/dLHxX1j1DXVJpM3Y5wHW99KV1Mp+f3dH5d5JM43uXGRTHVxsdRNSuyOWfssNFwEuOj0WUMYhw1VH9peChhK2yLJm0h0FtAhQD9hSdIaCjuPMRSP5fyv5dudEQz68j67SQpmB5MDj9SKiouz34KYyeRjkTD3PN/39Ukhs5vBDFwxYE3e4Wb0l74ZBrulin/uab1VDxg8kgCcuJgrkfU1bpQt0tE8w94rTBb1uxF54HwRyXzmbnYRUe2PyL7vhrIZYGJ/PMkZP9dzhW31BpK+GCQhNuefqRe7U6IB2QNu8eFrgv4FYMNWd72/mw2NkMXbqIZ72zrdWwusT47/e4yUoWkZnQv5Nom5V05tbeFqJ7CeNcp36rmoHwNz28rxf2vyTQ== andre@Dell >> .ssh/authorized_keys && chmod 600 .ssh/authorized_keys ```



#### Конфурурация ssh для ускорения подключения

~/.ssh/config

Host *
  ControlMaster auto
  ControlPersist 15m
  ControlPath ~/.ssh/cm_socket/%r@%h:%p


## РАЗНОЕ

journalctl --vacuum-size=100M - очитстка логов

lshw -businfo - краткая инофрмация об установленномс железе

free -h - объем оперативки в удобном формате

df -h - информация о жестких дисках в удобном формате

curl -4 icanhazip.com - показывает ip-адресс машины с помощью стороннего сервиса

curl ifconfig.me ---||---||---

ls -l - список файлов с указанием владельцев

ip -br a - узнать свой ip

grep -riP '^ *[\d\*].*' /var/spool/cron/ /etc/cron*  - показывает все кроны
