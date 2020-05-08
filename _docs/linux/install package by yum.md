---
order: 13
title: (LINUX) install package by yum
category: Linux
---

1. apache install(httpd)
yum install httpd

2. mysql install
yum install mysql

3. php install
yum install php

4. php-mysql install
yum install php-mysql

5. install library
yum -y install httpd mysql-server mysql php php-devel php-gd php-mbstring php-mysql php-pear php-pecl-mailparse 

---------------------------------------------------------------------------------------------------------------------

1. Apache 설치
  1) 설치 여부 체크
    yum list installed | grep http
      - 아래처럼 결과가 출력되면 설치되어 있는 것이다.
      httpd.i386      2.2.3-x       installed
    
  2) apache port가 떠있는지 확인
    netstat -lntp
      - 아래처럼 나오면 아파치가 떠있지 않은 것이다.
      ~~머라머라..
      tcp   0   0:::22      ::*         LISTEN      2219/sshd
      ~~머라머라..
  3) Apache 실행
    /usr/sbin/apachectl start
    
  4) 데몬이 정상적으로 실행되었는지 확인한다
    netstat -lntp
      ~~
      tcp     0   0:::80     :::*     LISTEN      3818/httpd
    
2. Mysql 설치
  1) 설치 여부 확인
    yum list installed | grep mysql
  2) mysql client 설치
    yum install mysql
  3) mysql server 설치
    yum install mysql-server
  4) server 구동
    /etc/rc.d/init.d/mysqld start
  5) password 변경
    /usr/bin/mysqladmin -u root password 'new password'
    
3. PHP 설치
  1) php 설치여부 확인
    which php
      /usr/bin/which: no php in 머라머라 나오면...php가 설치된 디렉토리를 못찾는다는 의미
    yum list installed | grep php   로 설치 여부 확인
  2) php 설치
    yum install php
  3) 그외 필요요소들 설치하자..
    yum -y install php-devel php-gd php-mbstring php-pear php-pecl-mailparse php-mysql mod_ssl
  4) 정상적인 설치 여부 확인
    which php
      /usr/bin/php 
    php -v
      PHP xxxxx ~~~
  5) 아파치의 php 설정에 다음줄을 추가해준다.
    vi /etc/httpd/conf.d/php.conf
      AddHandler php5-script .php
      AddType text/html .php
      AddType application/x-httpd-php .php .html .htm .inc  <- 추가
  6) 아파치 재실행
    /usr/sbin/apachectl restart
