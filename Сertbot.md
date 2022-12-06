
### выпуск сертификата


certbot certonly --cert-name games.apkinformer.com --webroot -w /var/www/games.apkinformer.com/ -d games.apkinformer.com,www.games.apkinformer.com - выпуск сертификата



###   проверка сертификата 
curl -vI --resolve proftracker.xyz:443:192.168.1.6 https://proftracker.xyz
echo | openssl s_client -servername 4mjlixyhcc.com -verify_hostname 4mjlixyhcc.com -verify 2 -connect 15.235.165.96:443 2>/dev/null | openssl x509 -noout -dates

