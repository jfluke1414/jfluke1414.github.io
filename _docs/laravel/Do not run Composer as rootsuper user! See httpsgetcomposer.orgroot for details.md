---   
 order: 4   
 title: (Laravel) Do not run Composer as rootsuper user! See httpsgetcomposer.orgroot for details
 category: Laravel   
---   
   
1. Error Do not run Composer as rootsuper user! See httpsgetcomposer.orgroot for details

Solution
export COMPOSER_ALLOW_SUPERUSER=1

2. Error
The openssl extension is required for SSL/TLS protection but is not available. If you can not enable the openssl extension, you can disable this error, at your own risk, by setting the 'disable-tls' option to true.

Solution
composer config -g -- disable-tls true

