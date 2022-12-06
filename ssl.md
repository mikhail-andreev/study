echo | openssl s_client -servername qewktvltio.com -verify_hostname qewktvltio.com -verify 2 -connect 192.168.1.7:443 2>/dev/null | openssl x509 -noout -dates

true | openssl s_client -showcerts -servername qewktvltio.com -verify_hostname -connect localhost:443 2>&1 | openssl x509 -noout -text -dates 

curl -vI --haproxy-protocol --resolve qewktvltio.com:443:localhost https://qewktvltio.com 2>&1 >/dev/null | grep -A 7 "Server certificate"


certbot certonly --cert-name proftracker.xyz --webroot -w /var/www/html --domains proftracker.xyz,56chj6nlyuwzd1jl.pw,snxr9coal0cyxl9g.pw,fyg2lg1qq0rgpl4q.art,sscfhzlx4t6fkkfw.com,699yrlpb75yaa.art,9wshcjxsjjy6da.art,fbtopobtokcwwd.com,lsgmmpzbipebxu.com,qewktvltio.com,waczjttdkl.com;