---
order: 11
title: (PHP-codeig) Install Codeigniter
category: Php - codeignitor
---

	1. Application, system 폴더 복사
	2. .htaccess 루트에 있어야 함.

//Httpconf 설정

ServerRoot "/etc/httpd"
Timeout 300
ServerName www.avds.co.kr:80
DocumentRoot "/home/avds"


<Directory />
#    Options FoillowSymLinks
#    AllowOverride None
#Require all granted
 
Order allow,deny
Allow from all
</Directory>
 



<Directory "/home/avds">
 Options FollowSymLinks
Order allow,deny
    Allow from all


#
# DirectoryIndex: sets the file that Apache will serve if a directory
# is requested.
#
<IfModule dir_module>
    DirectoryIndex index.html index.php
</IfModule>

AddType application/x-httpd-php .php .php3 .php4 .php5 .html .htm .inc



//Php.ini

short_open_tag = On

display_errors = Off

date.timezone = Asia/Seoul


///home/avds/.htaccess 루트 수정
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_URI} !^/js/(.*)$
RewriteCond %{REQUEST_URI} !^/css/(.*)$
RewriteCond %{REQUEST_URI} !^/images/(.*)$
RewriteCond %{REQUEST_URI} !^/font/(.*)$
RewriteRule ^(.*)$ /index.php/$1
</IfModule>
