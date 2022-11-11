## MYSQL

### Установка

sudo apt install mysql-server

mysql -u root -p -вход в мускл когда включена аутентификация root с помощью пароля

sudo mysql_secure_installation - запускает скрипт настройки безопасности

### Добавление пользователя 



mysql; -чтобы зайти в консоль мускуля.
SELECT host,user FROM mysql.user;  - посмотреть какие юзеры есть сейчас (мало ли, уже дали доступ)

SHOW DATABASES;  показать какие БД вообще присутствуют 

SELECT user,authentication_string,plugin,host FROM mysql.user;

FLUSH PRIVILEGES; - перезагрузка прав доступа пользователей

CREATE USER 'miha'@'localhost' IDENTIFIED BY 'password'; - создать пользователя
 
GRANT ALL PRIVILEGES ON *.* TO 'miha'@'localhost' WITH GRANT OPTION; - дать все права

CREATE USER 'games_apkinformer'@'%' IDENTIFIED BY 'UhTHzptgRzD5A8mjbNqnmt73RHqer9';

GRANT ALL PRIVILEGES ON games_apkinformer_com.* TO 'games_apkinformer'@'%' WITH GRANT OPTION;

GRANT SELECT ON 'bidnew_stage'.* TO 'vasiliy_shilov'@'%' IDENTIFIED BY 'password123321'; FLUSH PRIVILEGES; 

### Резервное копирование 

mysqldump -u USERNAME -pPASSWORD DBNAME > DBBACKUP.sql

mysqldump -u USERNAME -pPASSWORD --databases DB1 DB2 DB3.. >DBBACKUP.sql

mysqldump -u USERNAME -pPASSWORD --all-databases > ALLDBBACKUP.sql

mysqldump -u apkuser1000 -p4faksy8zzszdi1gs7yMtBJdJNr8LtzPF  apkinformer_com > DBBACKUP.sql

mysqldump -u apkuser1000  apkuser1000 > DBBACKUP.sql

-u — указывает ваше имя пользователя;
-p — указывает пароль;
DBNAME — имя базы данных, дамп которой вы создаете;
DBBACKUP.sql — имя файла создаваемой копии;
-h — указывает имя хоста сервера MySQL;
–Databases — определяет нужную базу данных;
-all-databases — необходим для дампа всего массива баз данных;
–Default-auth = plugin — используется для указания подключаемого модуля аутентификации на стороне клиента, который будет использоваться;
–Compress — применяется для включения сжатия в протоколе сервер/клиент;
-P — указывает номера порта, используемого для подключения к MySQL.

Чтобы экспортировать весь сервер MySQL, введите эту команду:

mysqldump -u your_username -p --all-databases

Если вы собираетесь хранить несколько резервных копий в одном месте, то будет удобно различать копии по их актуальности, если добавить текущую дату к имени файла резервной копии:

mysqldump database_name > database_name-$(date +%Y%m%d).sql

Восстановление базы:

mysql  database_name < file.sql

Параметр -all-databases используется для резервного копирования всего массива баз данных. Если вы хотите восстановить только одну базу данных из файла, где их сразу несколько, то можно сделать это с помощью --one-database:

mysql --one-database database_name < all_databases.sql
