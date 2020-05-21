---   
order: 69   
title: (LINUX) Phpinfo download 현상   
category: Linux   
---   
   
apache와 php를 설치한 후에 phpinfo가 정상적으로 출력되지 않는 경우가 있습니다.   
### 1. 일단 php가 잘 설치되었나 확인하기 위해   
cat /usr/local/apache/conf/httpd.conf |grep Doc < 아파치 루트경로를 찾아줍니다.   
ex) DocumentRoot “/usr/local/apache/htdocs”   
   
### 2. 해당경로에 phpinfo파일을 생성해줍니다.   
vi /usr/local/apache/htdocs/phpinfo.php   
내용은   
```
<?   
phpinfo();   
?> 
```
   
### 3. 브라우져 URL에 [IP주소]/phpinfo.php를 입력합니다.   
보통 APM의 정보가 출력되어야하나,   
소스코드 그대로 출력되는 경우가 종종있습니다.   
확인사항은 다음과 같습니다.   
1. apache에서 php의 모듈확인.   
vi /usr/local/apache/conf/httpd.conf   
LoadModule php5_module modules/libphp5.so < 이 모듈이 포함되어 있는지 확인합니다.   
2. apache에서 php의 확장자를 추가   
vi /usr/local/apache/conf/httpd.conf   
위 파일로 들어가서 아래처럼 확장자를 추가해줍니다.   
<IfModule mime_module>   
    AddType application/x-httpd-php .php   
    AddType application/x-httpd-php-source .phps   
  <IfModule>   
