---   
order: 92   
title: (LINUX) [LINUX NGINX] yum nginx 설치 방법   
category: Linux   
---   
   
nginx를 yum으로 설치하려고 하면 2014년 (2년쯤 전) 버젼으로 설치가 됩니다.    
centos의 epel에 있는 버젼이 좀 많이 늙어서 찜찜합니다.    
   
nginx의 docs를 보면 최근 mainline 버젼으로 설치하는 방법이 있습니다.    
http://nginx.org/en/linux_packages.html    
   
/etc/yum.repos.d에 nginx.repo 파일을 만들어서 아래 내용을 넣습니다.   
nginx는 mainline과 stable의 두가지 버젼이 있으며,   
stable이라고 stable이 아닌 것이므로 mainline을 설치 합니다.   
    
[nginx]    
name=nginx repo    
baseurl=http://nginx.org/packages/mainline/centos/6/$basearch/    
gpgcheck=0    
enabled=1    
   
centos 6 버젼인 경우은 아래와 같습니다. 숫자 7이 6으로 바뀝니다.    
   
[nginx]    
name=nginx repo    
baseurl=http://nginx.org/packages/mainline/centos/7/$basearch/    
gpgcheck=0    
enabled=1    
   
이후에는 쉽습니다.    
   
sudo yum install nginx    
    
   
2016.3월 기준으로 stable 버젼인 1.9.12 버젼이 설치 됩니다.    
stable 버젼은 repo가 다음과 같으며, 1.8.2 버젼이 설치 됩니다.   
    
[nginx]    
name=nginx repo    
baseurl=http://nginx.org/packages/centos/7/$basearch/    
gpgcheck=0    
enabled=1   
    
    
nginx를 시작 합니다.   
    
systemctl start nginx   
systemctl enable nginx   
    
    
nginx 설정파일은   
/etc/nginx   
    
디폴트 사용자 디렉토리는   
/usr/share/nginx/html   
    
    
/etc/nginx/conf.d/default.conf 파일을 수정 합니다.   
    
root /usr/share/nginx/html;    
index index.php index.html index.htm;    
   
location / {    
     try_files $uri $uri/ /index.php?$query_string;    
}    
   
...    
location ~ \.php$ {    
root /usr/share/nginx/html;    
fastcgi_pass 127.0.0.1:9000;    
fastcgi_index index.php;    
fastcgi_param SCRIPT_FILENAME $document_root/$fastcgi_script_name;    
include fastcgi_params;    
}    
}   
    
    
socket으로 운영하기 위해서는 /etc/opt/remi/php70/php-fpm.d/www.conf 를 수정해 주고   
    
listen = /var/run/php70-php-fpm.sock   
listen.owner = nginx    
listen.group = nginx   
    
/etc/nginx/conf.d/default.conf 의 fastastcgi_pass를 수정해 줍니다.   
    
fastfastcgi_pass 127.0.0.1:9000   
=> fastcgi_pass unix:/var/run/php70-php-fpm.sock    
    
수정이 다 끝나면 php70-php-fpm 과 nginx를 restart 해줍니다.   
    
systemctl restart php70-php-fpm   
systemctl restart nginx   
