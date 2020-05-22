---         
order: 102         
title: (LINUX) php server setting - codeignitor   
category: Linux         
---         
         
### php install with yum   
https://hack-cracker.tistory.com/159   
   
[Web server by using Yum]   
yum -y install httpd   
yum -y install php   
yum -y install php-mysql   
yum -y install mysql   
yum -y install mysql   
   
### php ini 설정   
https://sarc.io/index.php/httpd/140-2014-04-15-22-17-14   
   
-----------------------------------------------------------------------------------------------------------------------------   
   
### minimal일 경우 bash파일 수정   
vi .bash_profile    
PATH=$PATH:$HOME/bin:/sbin   
source .bash_profile   
   
-----------------------------------------------------------------------------------------------------------------------------   
vi /etc/sysconfig/network-scripts/ifcfg-ens32   
BOOTPROTO=static   
IPADDR=192.168.5.161   
NETMASK=255.255.255.0   
NETWORK=192.168.5.0   
   
vi /etc/sysconfig/network   
HOSTNAME=localhost.localdomain   
GATEWAY=192.168.5.1   
   
systemctl restart network   
   
vi /etc/resolv.conf   
nameserver 8.8.8.8   
nameserver 8.8.4.4   
   
   
firewall 등록 안되어있을시(Minimal)   
yum install firewalld   
systemctl start firewalld.service   
   
[firewall]   
firewall-cmd --permanent --zone=public --add-port=80/tcp   
firewall-cmd --permanent --zone=public --add-port=6502/tcp   
   
firewall-cmd --permanent --zone=public --add-port=22/tcp   
firewall-cmd --permanent --zone=public --add-port=3306/tcp   
firewall-cmd --permanent --zone=public --add-port=3690/tcp   
   
* 허용한 포트 목록   
firewall-cmd --list-ports   
   
systemctl restart firewalld.service   
   
-----------------------------------------------------------------------------------------------------------------------------   
   
### - yum   
yum groupinstall "Development tools"   
yum -y install net-tools   
yum -y remove mysql-libs    
yum -y install wget    
yum -y install openssl-devel pcre-devel     
   
### [install libraray]   
yum -y install bzip2 bzip2-devel bzip2-libs zlib-devel cmake ncurses-devel libjpeg-devel   
yum -y install libaio-devel libpng-devel libxml2*   
yum -y install libevent   
yum -y install expat-devel   
yum -y install epel-release   
yum -y install php-mcrypt   
yum -y install openssl-devel pcre-devel   
   
### [user management]   
useradd crypto   
   
cd /home   
chown root.root crypto   
--------------------------------------------------------------------------------   
### 1. apr   
wget https://www-eu.apache.org/dist//apr/apr-1.7.0.tar.gz   
./configure --prefix=/home/crypto   
cp -apr libtool libtoolT   
./configure --prefix=/home/crypto   
make    
make install   
--------------------------------------------------------------------------------   
### 2. apr util   
wget https://www-eu.apache.org/dist//apr/apr-util-1.6.1.tar.gz   
./configure --prefix=/home/crypto --with-apr=/home/crypto   
make   
make install   
   
--------------------------------------------------------------------------------   
### 3. libmcrypt   
wget http://app.nidc.kr/linux/lib/libmcrypt-2.5.8.tar.gz    
tar xvf libmcrypt-2.5.8.tar.gz   
cd libmcrypt-2.5.8   
   
./configure --prefix=/home/crypto --with-php-config=/home/crypto/bin/php-config   
   
make   
make install   
--------------------------------------------------------------------------------   
### 4. openssl    
wget https://www.openssl.org/source/openssl-1.0.2s.tar.gz   
./config --prefix=/home/crypto    
make    
make install   
   
--------------------------------------------------------------------------------   
### 5. Apache   
wget https://www-us.apache.org/dist//httpd/httpd-2.4.39.tar.gz   
   
cd /home/util   
tar xvf httpd/httpd-2.4.10.tar.gz   
   
./configure --prefix=/home/crypto --with-apr=/home/crypto --with-apr-util=/home/crypto --enable-unique-id --enable-dav --enable-dav-fs --enable-headers --enable-mods-shared=most --enable-ssl --enable-so --enable-module=so --enable-deflate --enable-http --with-openssl=/usr/include/openssl --libexecdir=/home/crypto/libexec   
make   
make install   
-------------------------------------------------------------------------------   
   
### 6. db   
wget https://downloads.mariadb.org/interstitial/mariadb-10.1.40/source/mariadb-10.1.40.tar.gz   
   
tar xvf mariadb-10.1.40.tar.gz    
   
cmake -DCMAKE_INSTALL_PREFIX=/home/crypto/ -DWITH_INNOBASE_STORAGE_ENGINE=1 -DWITH_ARCHIVE_STORAGE_ENGINE=1 -DWITH_BLACKHOLE_STORAGE_ENGINE=1 -DMYSQL_DATADIR=/home/cryptodb -DWITH_PERFSCHEMA_STORAGE_ENGINE=1 -DWITH_PARTITION_STORAGE_ENGINE=1 -DWITH_FEDERATEDX_STORAGE_ENGINE=1 -DWITH_ARIA_STORAGE_ENGINE=1 -DWITH_XTRADB_STORAGE_ENGINE=1 -DDEFAULT_CHARSET=utf8 -DDEFAULT_COLLATION=utf8_general_ci -DENABLED_LOCAL_INFILE=1 -DWITH_EXTRA_CHARSETS=all -DWITH_READLINE=1 -DWITH_SSL=system -DWITH_ZLIB=system   
   
make    
make install   
   
환경설정   
->데몬복사   
//cp /home/officedb/mariadb/support-files/mysql.server /etc/init.d/mariadb   
cp /home/crypto/support-files/mysql.server /etc/init.d/mariadb   
chkconfig --add mariadb   
About chkconfig ?   
mysql 이나 apache 같은 사용자가 설치한 프로그램 들을 부팅시 자동으로? 실행 하기 위해서 이 프로그램을 사용한다.   
   
->설정파일 복사   
cp /home/crypto/support-files/my-innodb-heavy-4G.cnf /home/crypto/my.cnf   
   
   
   
   
-> 계정추가   
adduser mysql   
adduser ncrypto   
adduser cryptoadm   
   
-> DB 생성   
/home/crypto/scripts/mysql_install_db --user=cryptoadm --basedir=/home/crypto/ --datadir=/home/cryptodb   
   
-> nbox 계정 mariadb 권한 설정(mysql로 무조건 해주어야 한다. 아니면 스타트가 되지 않는다.)   
chown mysql.mysql /home/cryptodb/ -R   
   
   
-> Error 발생 -> Job for mariadb.service failed. See ‘systemctl status mariadb.service‘ and ‘journalctl -xn’ for details.   
Cd /home/officedb/mariadb/data   
rm -rf ib*   
아래 파일들을 지워야함.   
-rw-rw----. 1 nbox nbox  77594624 Aug 18 10:39 ibdata1   
-rw-rw----. 1 nbox nbox 268435456 Aug 18 10:39 ib_logfile0   
-rw-rw----. 1 nbox nbox 268435456 Aug 18 10:39 ib_logfile1   
-rw-rw----. 1 nbox nbox 268435456 Aug 18 10:39 ib_logfile2   
   
systemctl start mariadb.service   
   
   
   
### [mysql 접속 권한]   
./mysql -u root -p   
Enter(비번이 없기때문에 엔터치면 그냥 접속)   
   
use mysql;   
>비번 설정   
update user set password=password('1234') where user='root';   
update user set password=password('1234') where user='ncrypto';   
   
   
INSERT INTO mysql.user (host,USER,password) VALUES ('13.58.191.130','root',password('1234'));   
grant all on *.* to root@'13.58.191.130' IDENTIFIED BY '1234';   
FLUSH PRIVILEGES;   
   
   
INSERT INTO mysql.user (host,USER,password) VALUES ('13.58.191.130','ncrypto',password('1234'));   
grant all on *.* to ncrypto@'13.58.191.130' IDENTIFIED BY '1234';   
FLUSH PRIVILEGES;   
   
[create database]   
./mysql -u root -p   
1234   
   
use mysql;   
create database cryptohard;   
   
//officehard.sql 있는 directory에서   
->import   
/home/crypto/bin/mysql -u ncrypto -p cryptohard < cryptohard.sql   
   
->export   
/home/crypto/bin/mysqldump -u ncrypto -p cryptohard > cryptohard.sql   
--------------------------------------------------------------------------------   
### 7. php   
   
///////wget https://www.php.net/distributions/php-7.3.7.tar.gz   
   
yum -y install libicu-devel.x86_64   
yum -y install php-intl   
yum -y install curl-devel   
   
export CFLAGS="-D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64"   
   
wget https://www.php.net/distributions/php-5.6.22.tar.gz   
   
tar xvf php-5.6.22.tar.gz   
   
   
./configure --prefix=/home/crypto --with-apxs2=/home/crypto/bin/apxs --with-openssl-dir=/home/crypto --enable-mbstring --enable-sockets --with-mysql=/home/crypto --with-gd --with-jpeg-dir=/usr/lib --with-png-dir=/usr/lib --with-zlib-dir=shared --enable-bcmath --enable-ftp --enable-so CFLAGS=-D_LARGEFILE_SOURCE --with-curl=/home/crypto/ --with-mysqli=/home/crypto --with-mysqli=/home/crypto/bin/mysql_config   
   
	   
php 재설치 원할경우(php는 덮어써진다. 아파치는 안된다.(아파치는 지우고 나서 다시 설치)) 순서는 아파치->php   
   
   
make clean < 컴파일했던 것을 모두 지웁니다.   
   
./configure 기존설정값+추가할설정값 < 기존설정값에 추가할설정값을 더해 명령어를 입력합니다.   
   
make   
make install   
   
   
------------------------------------------------------------------------------------------------------------------   
version patch   
tar -cvzf crypto_2020_2_20.tar.gz htdocs/   
   
------------------------------------------------------------------------------------------------------------------   
### GITHUB INSTALL   
   
wget https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.25.0.tar.gz   
   
tar -zxvf git-2.25.0.tar.gz   
make configure   
./configure --prefix=/home/crypto   
   
make   
   
make install   
   
   
--------------------------------------------------------------   
### GITHUB HOW TO USE   
   
1. CREATE   
git config --global user.name "Hyunjin Yeo"   
git config --global user.email jfluke1414@gmail.com   
   
   
2. make .git 파일   
cd /home/crypto/htdocs   
git init   
   
3. make vi file   
cd /home/crypto/htdocs   
vi README.md   
   
4. add project   
git add .   
   
5. upload   
git remote set-url origin git@github.com:jfluke1414/ar_crypto.git   
//git remote add origin https://jfluke1414@stash/scm/ar_crypto/repo.git   
   
git push origin master -f   
   
--------------------------------------------------------------------------------------------------------------   
   
### SSH 설정   
   
1. create   
ssh-keygen -t rsa -b 4096 -C "jfluke1414@gmail.com"   
   
Enter -> Enter -> Enter   
   
2. Copy    
cd /root/.ssh/   
   
cat id_rsa_pub   
   
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDhbZDH3ae4dAQCbU7/e6k1MRUlQpYvan092X90bTOz1VkP/A03/rZxcDgeC2clVBpCs6uX4YUqvK4w7mHr2A+yz1RG56plIzf3VDQDSltmZRF8T8+9MuxTpY/mBXdqyu3/BnrlYo2Bq2lIAiyc0/H+lcmcaseEhjpCH3azJzWyIuhJrhibEZkxTVXYN5juNdH/4tt3FTnnvz+eenwuZ2yjPOmgzCFP+YGO+pl/xb8BRHXBrvDKq9+rvtlnWWYrz272cnCyIEgjyC7cvitmQnRu8JKGsXQMdcWuJKPJgenxOa1b+zi5Q6dmLRGa+j6kAks4r1DirYUE1Ixf/86PV38lUwVnvD7SgYC22zlGTbUFMekLH1sSsnxbtFjsjXJ2c7nJgG6TbydFMlzHICxKHYpJR+GyLi5o8jfPCHdpwLwLpsrGidaJhR7C7CILWJVfQmpKhh0ka+iVBzEgdClZ+C7VYZl1LPMLT5vajrFDzUxa6XJ5SaiQOuOWRY/huIP3SP6k5WDRARXbHsGZugFpnD65ODFpF7pkISA5ICDogC8gNqTNUDx3pD1niXrjI70PVUPWRTP3VSdsCEAESaMsEl1x1kAcbhAZFKyhp3wymHSYFFVdxqcurh4SjIHDRnxQOOAxYC9Jy+AtiPPQnsffkXVAbdpuaK+Y0N3VKCDG0ot42Q== jfluke1414@gmail.com   
   
--------------------------------------------------------------------------------------------------------------   
### Amazone EC2 How to connect to instace from ssh tool   
   
### 1. Amazon EC2 instance 만들때 kep pair 만들거나 만들었던거 선택   
 - .pem 파일을 저장   
   
### 2. putty gen 실행   
### 3. load pem 파일   
### 4. save   
putty 사용시 : save private file(ppk 파일명)   
ex> jfluke1313.ppk   
   
xshell 사용시   
export Openssh key   
ex> jfluke1313.ppk   
   
   
### 5. xshell 설정   
- 호스트에 입력   
퍼블릭 DNS(IPv4)   
ec2-3-12-103-73.us-east-2.compute.amazonaws.com   
   
- Athentication   
Method : public key   
user : amazon -> instance -> connect -> 이게 유저 이름"ec2-user"   
   
ssh -i "jfluke1313.pem" ec2-user@ec2-3-12-103-73.us-east-2.compute.amazonaws.com   
   
- userkey setting -> jfluke1313.ppk 선택   
   
연결 끝.   
   
### root 계정 접속   
   
1. sudo passwd root   
setting pw   
   
2. su - root   
   
--------------------------------------------------------------------------------------------------------------   
### **Apache permission 문제   
/home/crypto 디렉토리 excutable이어야 한다.   
   
chmod 755 /home/crypto   
   
### **phpinfo.php 파일 다운로드 될때   
아파치 httpd.conf에 AddType을 확인해 보고, php.ini 에서 short open tag = on 으로 해놓았다면   
   
   
phpinfo파일에 <? phpinfo(); ?> 까지만 적어주자 <?php phpinfo(); ?> 로 하면 페이지 다운이 된다.   
   
--------------------------------------------------------------------------------   
### Memory swap 늘리기   
   
1.do things below in order   
fallocate -l 1GB /swapfile   
sudo dd if=/dev/zero of=/swapfile count=1024 bs=1MiB   
   
chmod 600 swapfile   
mkswap /swapfile   
swapon /swapfile   
free -m   
   
--------------------------------------------------------------------------------   
### Install SVN    
   
### 1. Create SVN user   
adduser svn   
passwd svn   
   
### 2. SVN 생성   
svnadmin create --fs-type fsfs /home/svn/crypto   
   
### 3. 그룹 소유자 변경   
cd /home/svn   
chown -R svn:svn /home/svn/crypto   
chown -R root:root /home/svn/crypto   
   
### 4. 설정파일 수정   
vi /home/svn/crypto/conf/svnserve.conf   
# 익명 사용자 읽기 사용 여부   
anon-access = read   
# 인증 사용자 쓰기 사용 여부   
auth-access = write   
# 인증에 사용될 패스워드 설정 파일   
password-db = passwd   
   
### 5. Start   
svnserve -d -r /home/svn/   
   
- check service   
ps -aux | grep svn   
   
### 6. bash_profile 수정   
vi ~/.bash_profile?   
   
추가/수정   
SVN_EDITOR=/usr/bin/vi   
export SVN_EDITOR   
   
source .bash_profile   
   
### 7.   
svn mkdir svn://13.58.191.130/crypto/trunk   
svn mkdir svn://ec2-13-58-191-130.us-east-2.compute.amazonaws.com/crypto/trunk   
   
svn mkdir svn://13.58.191.130/crypto/branches   
svn mkdir svn://13.58.191.130/crypto/tags   
   
1) :q!   
2) C    
3) enter   
   
   
### 8. checkout   
svn checkout svn://ec2-13-58-191-130.us-east-2.compute.amazonaws.com/crypto   
   
   
eclipse   
help -> install software   
add   
   
name : svn   
location : http://subclipse.tigris.org/update_1.10.x   
