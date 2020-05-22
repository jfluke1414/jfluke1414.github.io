---               
order: 104   
title: (LINUX) multiple virtual host setting   
category: Linux               
---               
               
### Virtual host 설정   
## 1. vi /home/crypto/conf/httpd.conf   
상단에 아래추가   
#virtual host   
Include /home/crypto/conf/original/extra/httpd-vhosts.conf   
   
추가   
Listen 8080   
   
중간에 아래 추가   
<Directory /home/crypto/htdocs/crypto/public>   
    AllowOverride All   
    #Options All   
    #Options ExecCGI   
    #Order allow,deny   
    #Allow from all   
    Require all granted   
    AddHandler text/xml .xml   
    AddType application/x-httpd-php .php   
   
    # tpw   
    #SSLRequireSSL   
    # /tpw   
</Directory>   
   
   
<Directory /home/crypto/htdocs/portfolio/public>   
    Options Indexes FollowSymLinks   
    AllowOverride All   
    #Options All   
    #Options ExecCGI   
    #Order allow,deny   
    #Allow from all   
    Require all granted   
    AddHandler text/xml .xml   
    AddType application/x-httpd-php .php   
   
    # tpw   
    #SSLRequireSSL   
    # /tpw   
</Directory>   
   
   
   
## 2. vi /home/crypto/conf/original/extra/httpd-vhosts.conf   
아래와 같이 변경   
<VirtualHost *:80>   
    ServerAdmin localhost   
    DocumentRoot "/home/crypto/htdocs/crypto/public"   
    ServerName localhost   
    ServerAlias www.dummy-host.example.com   
    #ErrorLog "logs/dummy-host.example.com-error_log"   
    #CustomLog "logs/dummy-host.example.com-access_log" common   
</VirtualHost>   
   
<VirtualHost *:8080>   
    ServerAdmin localhost   
    DocumentRoot "/home/crypto/htdocs/portfolio/public"   
    ServerName localhost   
    #ErrorLog "logs/dummy-host2.example.com-error_log"   
    #CustomLog "logs/dummy-host2.example.com-access_log" common   
</VirtualHost>   
   
   
   
