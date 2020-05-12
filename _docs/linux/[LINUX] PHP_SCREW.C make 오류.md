---
order: 75
title: (LINUX) [LINUX] PHP_SCREW.C make 오류
category: Linux
---

* 설명
php_screw 모듈을 설치하면 php 소스를 암호화 할 수 있다.
php 가 설치되어 있는 상태에서 모듈만 추가한다.
 
* 소스 다운로드
wget http://sourceforge.net/projects/php-screw/files/php-screw/1.5/php_screw-1.5.tar.gz
 
* 설치
[root@ php_screw-1.5]# phpize
Configuring for:
PHP Api Version: 20041225
Zend Module Api No: 20060613
Zend Extension Api No: 220060519

[root@ php_screw-1.5]# ./configure
[root@ php_screw-1.5]# make && make install
 

make 에러
/usr/local/src/php_screw-1.5/php_screw.c: In function 'pm9screw_compile_file':
/usr/local/src/php_screw-1.5/php_screw.c:78: error: too few arguments to function 'org_compile_file'
/usr/local/src/php_screw-1.5/php_screw.c:84: error: too few arguments to function 'org_compile_file'
/usr/local/src/php_screw-1.5/php_screw.c:93: error: too few arguments to function 'org_compile_file'
make: *** [php_screw.lo] 오류 1
php_screw.c 파일의 78,84,93 라인을 수정해줍니다.
org_compile_file(file_handle, type);                                 < 수정 전
org_compile_file(file_handle, type TSRMLS_CC);         < 수정 후
 
그리고 make clean, 다시 make 를 진행합니다.
 
Installing shared extensions: /usr/local/php/lib/php/extensions/no-debug-non-zts-20060613/
위와같이 /usr/local/php/lib/php/extensions/no-debug-non-zts-20060613 에 모듈이 설치되었다고 나온다.
php_screw.so 파일을 /usr/local/php/lib/extension 로 복사.
