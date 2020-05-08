---
order: 16
title: (LINUX) CentOS _ Mysql installation by yum
category: Linux
---
1. yum 방식을 이용한 설치
[의존성 패키지]
mysql / mysql-server / mysql-connector-odbc / mysql-devel
yum -y install mysql mysql-server mysql-connector-odbc mysql-devel
-y 옵션은 [yes/no] 선택시 자동으로 yes를 처리하게해주는 옵션
2. 설정파일 복사
# cp /usr/share/mysql/my-huge.cnf /etc/my.cnf
설치되는 서버의 메모리용량에 따라 최적화된 설정파일을 복사해준다. 보통 2G이상의 메모리를 설치하므로 my-huge.cnf를 복사한다.
my-huge.cnf 1~2G
my-large.cnf 512M
my-medium.cnf 128M~ 256M
my-small.cnf 64M 이하
** UTF8 인코딩 셋을 사용하기 위한 설정파일 내용 변경
# vi /etc/my.cnf
[client]
default-character-set = utf8
[mysqld]
init_connect = SET collation_connection = utf8_general_ci
init_connect = SET NAMES utf8
default-character-set = utf8
character-set-server = utf8
collation-server = utf8_general_ci
[mysqldump]
default-character-set=utf8
[mysql]
default-character-set=utf8
3. DB파일 설치경로
/var/lib/mysql/mysql/ 경로아래에 DB파일이 위치한다.
4. 기본 mysql DB 인스톨 및 권한 변경
mysql_install_db && chown -R mysql:mysql /var/lib/mysql/
5. mysql 데몬 실행
ㄱ) 직접 실행
/etc/rc.d/init.d/mysqld start
/etc/rc.d/init.d/mysqld stop
/etc/rc.d/init.d/mysqld restart
ㄴ) 서비스 등록
chkconfig — add mysqld
chkconfig –level 2345 mysqld on
chmod 755 /etc/rc.d/init.d/mysqld
ㄷ) 자동서비스 선택
[root@localhost test]# ntsysv
[*] mysqld
7. 패스워드 변경 및 등록
ㄱ) sql 에서 실행
mysql > update user set password = password(‘비밀번호’) where user = ‘사용자’;
mysql > flush privileges; (* 적용하기)
ㄴ) 명령어 실행
#mysqladmin -u 사용자 password 비밀번호
8. sql script 실행

#mysql -u 사용자 -p 비밀번호 mysql < 파일명.sql