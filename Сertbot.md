
### выпуск сертификата

certbot certonly --cert-name games.apkinformer.com --webroot -w /var/www/games.apkinformer.com/ -d games.apkinformer.com,www.games.apkinformer.com

certbot certonly --cert-name proftracker.xyz --webroot -w /var/www/html --domains proftracker.xyz,56chj6nlyuwzd1jl.pw,snxr9coal0cyxl9g.pw,fyg2lg1qq0rgpl4q.art,sscfhzlx4t6fkkfw.com,699yrlpb75yaa.art,9wshcjxsjjy6da.art,fbtopobtokcwwd.com,lsgmmpzbipebxu.com,qewktvltio.com,waczjttdkl.com;


###   проверка сертификата 
curl -vI --resolve proftracker.xyz:443:192.168.1.6 https://proftracker.xyz
echo | openssl s_client -servername 4mjlixyhcc.com -verify_hostname 4mjlixyhcc.com -verify 2 -connect 15.235.165.96:443 2>/dev/null | openssl x509 -noout -dates
true | openssl s_client -showcerts -servername qewktvltio.com -verify_hostname -connect localhost:443 2>&1 | openssl x509 -noout -text -dates 
