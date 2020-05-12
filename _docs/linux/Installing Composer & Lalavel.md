---
order: 99
title: (LINUX) Installing Composer & Lalavel
category: Linux
---

0. Install PHP CLI(command line interface)
yum install php-cli php-zip wget unzip

1. Download the Composer installer
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"

2. To verify the data integrity of the script compare the script SHA-384
HdASH="$(wget -q -O - https://composer.github.io/installer.sig)"

3. run
php -r "if (hash_file('SHA384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"

php composer-setup.php --install-dir=/usr/local/bin --filename=composer

*If the hashes match, the following message will be shown:
Installer verified
1번부터 다시 실행

	 
4. install Composer in the /usr/local/bin directory:
php composer-setup.php --install-dir=/usr/local/bin --filename=composer
	
5. 확인
composer
