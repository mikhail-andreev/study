## MYSQL

mysql -u root -p -вход в мускл когда включена аутентификация root с помощью пароля

sudo mysql_secure_installation - запускает скрипт настройки безопасности

mysqldump -u root -p db_name > /db_backup.sql

SELECT user,authentication_string,plugin,host FROM mysql.user;

FLUSH PRIVILEGES; - перезагрузка прав доступа пользователей

CREATE USER 'miha'@'localhost' IDENTIFIED BY 'password'; - создать пользователя
 
GRANT ALL PRIVILEGES ON *.* TO 'miha'@'localhost' WITH GRANT OPTION; - дать все права


## Добавление пользователя 

mysql;

чтобы зайти в консоль мускуля.
SELECT host,user FROM mysql.user; 
чтобы посмотреть какие юзеры есть сейчас (мало ли, уже дали доступ)

SHOW DATABASES; 

#чтобы показать какие БД вообще присутствуют и спросить юзера к какой БД ему вообще нужен доступ _(в случае adsbid_stage это будет скорее всего bidnew_stage)_

GRANT SELECT ON 'bidnew_stage'.* TO 'vasiliy_shilov'@'%' IDENTIFIED BY 'password123321'; FLUSH PRIVILEGES; 
