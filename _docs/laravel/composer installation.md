---   
 order: 2   
 title: (Laravel) composer installation
 category: Laravel   
---   
   
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