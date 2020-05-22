---   
 order: 3   
 title: (Laravel) Laravel installation 
 category: Laravel   
---   
   
### Laravel install

cd /home/crypto/htdocs

### 1. create a project
composer create-project laravel/laravel --prefer-dist crypto

Homepage
composer create-project laravel/laravel --prefer-dist portfolio

### 2. configuration
chmod -R 777 /home/crypto/htdocs/crypto/storage
chmod -R 775 /home/crypto/htdocs/crypto/bootstrap
//chmod -R 775 /home/crypto/htdocs/crypto/vendor

### 3. start 
php artisan serve

### 4. controller 만들기
php artisan make:controller ContactController

### Setting
/home/crypto/conf/httpd.conf
Documentroot = /home/crypto/htdoc/crypto/public

### Error
## error ->PHP Warning:  require(/home/crypto/htdocs/crypto/bootstrap/../vendor/autoload.php): failed to open stream: No such file or directory in /home/crypto/htdocs/crypto/bootstrap/autoload.php on line 17
PHP Fatal error:  require(): Failed opening required '/home/crypto/htdocs/crypto/bootstrap/../vendor/autoload.php' (include_path='.:/usr/share/pear:/usr/share/php') in /home/crypto/htdocs/crypto/bootstrap/autoload.php on line 17
solution
composer update --no-scripts

## composer 업데이트시 아래 오류남. 설치 필요
## error -> the requested PHP extension mbstring is missing from your system.
solution
yum install php-mbstring

## error -> the requested PHP extension dom is missing from your system.
solution
yum install php-xml

## error -> PHP Fatal error:  Class 'PDO' not found in /home/crypto/htdocs/crypto/config/database.php on line 16
solution
yum install php-pdo
yum install php-pdo_mysql

cp /usr/lib64/php/modules/pdo.so /home/crypto/lib/php/extensions/
cp /usr/lib64/php/modules/pdo_sqlite.so /home/crypto/lib/php/extensions/
cp /usr/lib64/php/modules/pdo_mysqlnd.so /home/crypto/lib/php/extensions/

## error -> Use of undefined constant MCRYPT_RIJNDAEL_128 

yum install php-pear

## error -> 
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

## error ->not found mcrypt.h
solution
yum -y install libmcrypt-devel

## error -> 500 error
solution
cd /home/crypto/htdocs/crypto
cp .env.example .env
php artisan key:generate
php artisan config:cache

## Install npm
yum install npm
cd /home/crypto/htdocs/crypto
npm install

npm run dev
npm run watch


### When do you need installation of that library below
### 1. Zip
cd /home/util/php-7.0.10/ext/zip
/home/crypto/bin/phpize
./configure --prefix=/home/crypto --with-php-config=/home/crypto/bin/php-config
make
make & install

cd /home/crypto/lib/php/extensions/no-debug-zts-20151012/
mv mv zip.so ../

vi /home/crypto/lib/php.ini
extension=zip.so

### 1. 페이지 이동시(web.php) 아래 오류시
Error -> The requested URL /services was not found on this server.
solution - >
LoadModule rewrite_module libexec/mod_rewrite.so
httpd.conf에서 #주석 삭제 처리
그리고 apache 재시작