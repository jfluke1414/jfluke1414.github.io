---   
order: 107   
title: (LINUX) configure error Cannot find OpenSSL's evp.h   
category: Linux                        
---                        

## 1. Error OpenSSL's evp.h   
find / -name evp.h   
   
cd /home/util/php-7.3.21/ext/mysqlnd   
vi configure   
   
on the command :    
PHP_OPENSSL_DIR="/usr"   
export PHP_OPENSSL_DIR   
   
      
## 2. Error Cannot find OpenSSL’s libraries.   
find / -name libsso.so   
   
on the command :    
PHP_OPENSSL_DIR="/usr /usr/lib64"   
export PHP_OPENSSL_DIR   
   
## 3. execute configure on the directory   
cd /home/util/php-7.3.21/ext/mysqlnd   
./configure --prefix=/home/crypto --with-php-config=/home/crypto/bin/php-config --with-libdir=""   
