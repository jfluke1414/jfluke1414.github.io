---            
order: 103            
title: (LINUX) php server setting - laravel      
category: Linux            
---            
            
### php install with yum   
   
### [Web server by using Yum]   
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
yum -y install firewalld   
systemctl start firewalld.service   
   
[firewall]   
firewall-cmd --permanent --zone=public --add-port=80/tcp   
firewall-cmd --permanent --zone=public --add-port=8080/tcp   
firewall-cmd --permanent --zone=public --add-port=6502/tcp   
firewall-cmd --permanent --zone=public --add-port=8000/tcp   
   
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
yum -y install bzip2 bzip2-devel bzip2-libs zlib-devel cmake ncurses-devel libjpeg-devel libaio-devel libpng-devel libxml2* libevent expat-devel epel-release php-mcrypt   
   
yum -y install gcc freetype-devel libxml2-devel libmcrypt-devel pkgconfig bzip2-devel libpng-devel libpng-devel libjpeg-devel libXpm-devel gmp-devel aspell-devel recode-devel   
   
### [user management]   
useradd crypto   
   
cd /home   
chown root.root crypto   
chmod 755 crypto/   
mkdir cryptologs   
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
./config --prefix=/home/crypto --openssldir=/home/crypto   
make   
make install   
   
--------------------------------------------------------------------------------   
### 4. libzip    
wget https://libzip.org/download/libzip-1.2.0.tar.gz   
./config --prefix=/home/crypto    
make   
make install   
   
--------------------------------------------------------------------------------   
### 4. openssl    
wget https://www.openssl.org/source/openssl-1.0.2s.tar.gz   
./config --prefix=/home/crypto    
make   
make install   
   
--------------------------------------------------------------------------------   
### 5. [webp] 설치 완료 ok   
wget http://downloads.webmproject.org/releases/webp/libwebp-0.4.2.tar.gz   
./configure --enable-shared --prefix=/home/crypto   
make    
make install   
   
--------------------------------------------------------------------------------   
### 6. Apache   
wget https://www-us.apache.org/dist//httpd/httpd-2.4.39.tar.gz   
   
cd /home/util   
tar xvf httpd/httpd-2.4.10.tar.gz   
   
./configure --prefix=/home/crypto --with-apr=/home/crypto --with-apr-util=/home/crypto --enable-unique-id --enable-dav --enable-dav-fs --enable-headers --enable-mods-shared=most --enable-ssl --enable-so --enable-module=so --enable-deflate --enable-http --with-openssl=/usr/include/openssl --libexecdir=/home/crypto/libexec   
make   
make install   
-------------------------------------------------------------------------------   
   
### 7. db   
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
### 8. php   
   
///////wget https://www.php.net/distributions/php-7.3.7.tar.gz   
   
yum -y install libicu-devel.x86_64 php-intl curl-devel oniguruma gcc-c++ gcc   
   
yum -y install libtool-ltdl-devel pkg-config libevent-devel   
   
export CFLAGS="-D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64"   
   
------------------------------------------------------------------------------------------------------------------------   
### php5   
   
wget https://www.php.net/distributions/php-5.6.22.tar.gz   
   
tar xvf php-5.6.22.tar.gz   
   
   
./configure --prefix=/home/crypto --with-apxs2=/home/crypto/bin/apxs --with-openssl-dir=/home/crypto --enable-sockets --with-mysql=/home/crypto --with-gd --with-jpeg-dir=/usr/lib --with-png-dir=/usr/lib --with-zlib-dir=shared --enable-bcmath --enable-ftp --enable-so CFLAGS=-D_LARGEFILE_SOURCE --with-curl=/home/crypto/ --with-mysqli=/home/crypto --with-mysqli=/home/crypto/bin/mysql_config --disable-pdo --with-pic --enable-mbstring --enable-shared --enable-pic --with-onig=/home/crypto   
   
------------------------------------------------------------------------------------------------------------------------------------------------------   
   
### Install oniguruma 설치해야 될 시   
1. 다운로드   
여기에서 https://github.com/kkos/oniguruma   
다운로드 받아서 압축푼 후, 서버에 디렉토리 만들어서 Filezila로 파일들 보내준다.   
   
명령어 차례로   
1. autoreconf -vfi (* case: configure script is not found.)   
   
2. ./configure --prefix=/home/crypto   
   
3. make   
   
4. make install   
   
5. uninstall 시   
1. uninstall   
   
   
2. make uninstall   
   
   
------------------------------   
export CFLAGS="-D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64 -fPIC"   
   
### php7   
   
   
   
다운로드(php 7.0.10 다운받음 7.2부터는 mcrypt가 포함안되어 잇음)   
wget https://us2.php.net/distributions/php-7.3.13.tar.xz --no-check-certificate && tar -xvf php-7.3.13.tar.xz && cd php-7.3.13   
   
export PKG_CONFIG_PATH=/home/crypto/lib/pkgconfig   
   
original(오류생김)   
./configure shared --prefix=/home/crypto --with-apxs2=/home/crypto/bin/apxs --with-openssl-dir=/home/crypto --enable-mbstring --enable-sockets --with-gd --with-jpeg-dir=/usr/lib --with-png-dir=/usr/lib --with-zlib-dir=shared --enable-ftp --with-curl=/home/crypto/ --with-mysqli=/home/crypto/bin/mysql_config --without-sqlite3 --disable-pdo   
   
   
openssl 있고 없고 차이//--with-openssl-dir=/home/crypto (정상실행)   
./configure --prefix=/home/crypto --with-apxs2=/home/crypto/bin/apxs --enable-mbstring --enable-sockets --with-gd --with-jpeg-dir=/usr/lib --with-png-dir=/usr/lib --with-zlib-dir=shared --enable-ftp --with-curl=/home/crypto/ --with-mysqli=/home/crypto/bin/mysql_config --with-pic --enable-shared   
//--without-sqlite3 --disable-pdo   
   
CFLAGS=-fPIC   
php 재설치 원할경우(php는 덮어써진다. 아파치는 안된다.(아파치는 지우고 나서 다시 설치)) 순서는 아파치->php   
   
   
make clean < 컴파일했던 것을 모두 지웁니다.   
   
./configure 기존설정값+추가할설정값 < 기존설정값에 추가할설정값을 더해 명령어를 입력합니다.   
   
make   
make install   
   
------------------------------------------------------------------------------------------------------------------   
### sqlite   
wget https://www.sqlite.org/2020/sqlite-autoconf-3310100.tar.gz   
tar -zxvf sqlite-autoconf-3310100.tar.gz   
   
./configure --prefix=/home/crypto   
make   
make install   
   
------------------------------------------------------------------------------------------------------------------   
   
### version patch   
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
   
1. make .git 파일   
해당 프로젝트 디렉토리 이동 후 차례대로   
cd /home/crypto/htdocs/portfolio   
echo "# ar_portfolio" >> README.md   
git init   
git add README.md   
git commit -m "first commit"   
git remote add origin https://github.com/jfluke1414/ar_portfolio.git   
git push -u origin master   
   
2.   
git add .   
git commit -m "first update"   
git push   
   
3. CREATE   
git config --global user.name "Hyunjin Yeo"   
git config --global user.email jfluke1414@gmail.com   
   
4. git pull   
-----------------------------------------------------------------------------   
…or create a new repository on the command line   
echo "# ar_portfolio" >> README.md   
git init   
git add README.md   
git commit -m "first commit"   
git remote add origin https://github.com/jfluke1414/ar_portfolio.git   
git push -u origin master   
                   
…or push an existing repository from the command line   
git remote add origin https://github.com/jfluke1414/ar_portfolio.git   
git push -u origin master   
…or import code from another repository   
You can initialize this repository with code from a Subversion, Mercurial, or TFS project.   
   
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
   
1. Amazon EC2 instance 만들때 kep pair 만들거나 만들었던거 선택   
 - .pem 파일을 저장   
   
2. putty gen 실행   
3. load pem 파일   
4. save   
putty 사용시 : save private file(ppk 파일명)   
ex> jfluke1313.ppk   
   
xshell 사용시   
export Openssh key   
ex> jfluke1313.ppk   
   
   
5. xshell 설정   
- 호스트에 입력   
퍼블릭 DNS(IPv4)   
ec2-3-12-103-73.us-east-2.compute.amazonaws.com   
   
- Athentication   
Method : public key   
user : amazon -> instance -> connect -> 이게 유저 이름"ec2-user"   
   
ssh -i "jfluke1313.pem" ec2-user@ec2-3-12-103-73.us-east-2.compute.amazonaws.com   
   
- userkey setting -> jfluke1313.ppk 선택   
   
연결 끝.   
   
root 계정 접속   
   
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
   
   
### httpd.config 설정   
1. ServerRoot "/home/crypto"   
   
2. php5 or php7   
LoadModule php5_module        libexec/libphp5.so   
LoadModule php7_module        libexec/libphp7.so   
   
3.<Directory /> 수정   
   
<Directory />   
    AllowOverride All   
    Options All   
    Options ExecCGI   
    #Order allow,deny   
    #Allow from all   
    Require all granted   
    AddHandler text/xml .xml   
    AddType application/x-httpd-php .php   
   
    # tpw   
    #SSLRequireSSL   
    # /tpw   
</Directory>   
   
4.DocumentRoot 설정   
DocumentRoot "/home/crypto/htdocs"   
   
5. 디렉토리 설정   
<Directory "/home/crypto/htdocs">   
    #   
    # Possible values for the Options directive are "None", "All",   
    # or any combination of:   
    #   Indexes Includes FollowSymLinks SymLinksifOwnerMatch ExecCGI MultiViews   
    #   
    # Note that "MultiViews" must be named *explicitly* --- "Options All"   
    # doesn't give it to you.   
    #   
    # The Options directive is both complicated and important.  Please see   
    # http://httpd.apache.org/docs/2.4/mod/core.html#options   
    # for more information.   
    #   
    Options Indexes FollowSymLinks   
   
    #   
    # AllowOverride controls what directives may be placed in .htaccess files.   
    # It can be "All", "None", or any combination of the keywords:   
    #   AllowOverride FileInfo AuthConfig Limit   
    #   
    AllowOverride All   
   
    #   
    # Controls who can get stuff from this server.   
    #   
    Require all granted   
</Directory>   
   
   
Error phpinfo.php 실행시 실행되지 않을때   
위에 3번 <Directory /> 수정 해주고   
/home/crypto/bin apachectl stop   
/home/crypto/bin apachectl start   
apache restart   
   
   
   
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
   
1. Create SVN user   
adduser svn   
passwd svn   
   
2. SVN 생성   
svnadmin create --fs-type fsfs /home/svn/crypto   
   
3. 그룹 소유자 변경   
cd /home/svn   
chown -R svn:svn /home/svn/crypto   
chown -R root:root /home/svn/crypto   
   
4. 설정파일 수정   
vi /home/svn/crypto/conf/svnserve.conf   
# 익명 사용자 읽기 사용 여부   
anon-access = read   
# 인증 사용자 쓰기 사용 여부   
auth-access = write   
# 인증에 사용될 패스워드 설정 파일   
password-db = passwd   
   
5. Start   
svnserve -d -r /home/svn/   
   
- check service   
ps -aux | grep svn   
   
6. bash_profile 수정   
vi ~/.bash_profile?   
   
추가/수정   
SVN_EDITOR=/usr/bin/vi   
export SVN_EDITOR   
   
source .bash_profile   
   
7.   
svn mkdir svn://13.58.191.130/crypto/trunk   
svn mkdir svn://ec2-13-58-191-130.us-east-2.compute.amazonaws.com/crypto/trunk   
   
svn mkdir svn://13.58.191.130/crypto/branches   
svn mkdir svn://13.58.191.130/crypto/tags   
   
1) :q!   
2) C    
3) enter   
   
   
8. checkout   
svn checkout svn://ec2-13-58-191-130.us-east-2.compute.amazonaws.com/crypto   
   
   
eclipse   
help -> install software   
add   
   
name : svn   
location : http://subclipse.tigris.org/update_1.10.x   
   
   
------------------------------------------------------------------------------   
### install composer    
yum update   
yum install epel-release yum-utils -y   
yum -y install http://rpms.remirepo.net/enterprise/remi-release-7.rpm    
yum-config-manager --enable remi-php70   
yum install php   
   
0. Install PHP CLI(command line interface)   
yum -y install php-cli php-zip unzip wget   
   
1. Download the Composer installer   
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"   
   
2. To verify the data integrity of the script compare the script SHA-384   
HASH="$(wget -q -O - https://composer.github.io/installer.sig)"   
   
3. run   
php -r "if (hash_file('SHA384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"   
   
*If the hashes match, the following message will be shown:   
Installer verified   
1번부터 다시 실행   
   
?   
4. install Composer in the?/usr/local/bin?directory:   
php composer-setup.php --install-dir=/usr/local/bin --filename=composer   
	   
5. 확인   
composer   
   
출처: <https://linuxize.com/post/how-to-install-and-use-composer-on-centos-7/   
   
   
------------------------------------------------------------------------------   
### Laravel install   
   
cd /home/crypto/htdocs   
   
1. create a project   
composer create-project laravel/laravel --prefer-dist crypto   
   
Homepage   
composer create-project laravel/laravel --prefer-dist portfolio   
   
2. configuration   
chmod -R 777 /home/crypto/htdocs/crypto/storage   
chmod -R 775 /home/crypto/htdocs/crypto/bootstrap   
//chmod -R 775 /home/crypto/htdocs/crypto/vendor   
   
3. start    
php artisan serve   
   
4. controller 만들기   
php artisan make:controller ContactController   
   
Setting   
/home/crypto/conf/httpd.conf   
Documentroot = /home/crypto/htdoc/crypto/public   
   
Error   
error ->PHP Warning:  require(/home/crypto/htdocs/crypto/bootstrap/../vendor/autoload.php): failed to open stream: No such file or directory in /home/crypto/htdocs/crypto/bootstrap/autoload.php on line 17   
PHP Fatal error:  require(): Failed opening required '/home/crypto/htdocs/crypto/bootstrap/../vendor/autoload.php' (include_path='.:/usr/share/pear:/usr/share/php') in /home/crypto/htdocs/crypto/bootstrap/autoload.php on line 17   
solution   
composer update --no-scripts   
   
composer 업데이트시 아래 오류남. 설치 필요   
error -> the requested PHP extension mbstring is missing from your system.   
solution   
yum install php-mbstring   
   
error -> the requested PHP extension dom is missing from your system.   
solution   
yum install php-xml   
   
error -> PHP Fatal error:  Class 'PDO' not found in /home/crypto/htdocs/crypto/config/database.php on line 16   
solution   
yum install php-pdo   
yum install php-pdo_mysql   
   
cp /usr/lib64/php/modules/pdo.so /home/crypto/lib/php/extensions/   
cp /usr/lib64/php/modules/pdo_sqlite.so /home/crypto/lib/php/extensions/   
cp /usr/lib64/php/modules/pdo_mysqlnd.so /home/crypto/lib/php/extensions/   
   
error -> Use of undefined constant MCRYPT_RIJNDAEL_128    
   
yum install php-pear   
   
error ->    
solution   
find / -name mcrypt   
cd /home/util/php-5.6.22/ext/mcrypt/   
/home/crypto/bin/phpize   
./configure --prefix=/home/crypto --with-php-config=/home/crypto/bin/php-config   
make   
make install   
   
extension 설정   
Installing shared extensions:     /home/crypto/lib/php/extensions/no-debug-zts-20131226/   
cd /home/crypto/lib/php/extensions/no-debug-zts-20131226/   
cp mcrypt.so ../   
   
php.ini 추가   
extension=mcrypt.so   
   
error ->not found mcrypt.h   
solution   
yum -y install libmcrypt-devel   
   
error -> 500 error   
solution   
cd /home/crypto/htdocs/crypto   
cp .env.example .env   
php artisan key:generate   
php artisan config:cache   
   
### Install npm   
yum install npm   
cd /home/crypto/htdocs/crypto   
npm install   
   
npm run dev   
npm run watch   
   
   
### When do you need installation of that library below   
1. Zip   
cd /home/util/php-7.0.10/ext/zip   
/home/crypto/bin/phpize   
./configure --prefix=/home/crypto --with-php-config=/home/crypto/bin/php-config   
make   
make & install   
   
cd /home/crypto/lib/php/extensions/no-debug-zts-20151012/   
mv mv zip.so ../   
   
vi /home/crypto/lib/php.ini   
extension=zip.so   
   
   
Error -> Call to undefined function Illuminate\Encryption\openssl_cipher_iv_length()   
1. Openssl   
cd /home/util/php-7.0.10/ext/openssl   
   
error -> Cannot find config.m4.    
Make sure that you run '/home/crypto/bin/phpize' in the top level source directory of the module   
solution   
cp config0.m4 config.m4   
   
Error -> relocation R_X86_64_32 against 'rodata'(export CXXFLAGS=-shared-fPIC 해줘야 한다)   
   
/home/crypto/bin/phpize   
export CXXFLAGS=-shared-fPIC   
./configure --prefix=/home/crypto --with-php-config=/home/crypto/bin/php-config --with-openssl=/usr/lib64/openssl    
make   
make & install   
   
cd /home/crypto/lib/php/extensions/no-debug-zts-20151012/   
mv openssl.so ../   
   
vi /home/crypto/lib/php.ini   
extension=zip.so   
   
   
   
------------------------------------------------------------------------------------------------   
### 1. 페이지 이동시(web.php) 아래 오류시   
Error -> The requested URL /services was not found on this server.   
solution - >   
LoadModule rewrite_module libexec/mod_rewrite.so   
httpd.conf에서 #주석 삭제 처리   
그리고 apache 재시작   
   
   
------------------------------------------------------------------------------------------------   
### Virtual host 설정   
1. vi /home/crypto/conf/httpd.conf   
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
   
   
   
2. vi /home/crypto/conf/original/extra/httpd-vhosts.conf   
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
   
   
   
