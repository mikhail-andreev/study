## NGINX

sudo chown -R $USER:$USER /var/www/your_domain/html - назначение владения дирркторией, нужно для того чтобы была возможность чтения/записи

sudo chmod -R 755 /var/www/site.ru - установка прав доступа

sudo vim /etc/nginx/sites-available/your_domain - создание файла с директивами для запуска сервера

sudo ln -s /etc/nginx/sites-available/your_domain /etc/nginx/sites-enabled/ - создание файловой ссылки на диррективы, чтобы nginx подтянул их при запуске

sudo nginx -t - проверка синтаскиса конфигурационных файлов nginx

sudo nginx -s reload - мягкая перезагрузка Nginx
