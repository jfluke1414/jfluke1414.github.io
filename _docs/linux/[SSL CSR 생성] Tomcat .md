---   
order: 51   
title: (LINUX) [SSL CSR 생성] Tomcat    
category: Linux   
---   
   
### 1. Keystore 생성 명령어 : keytool -genkey -alias tapacross -keyalg RSA -keysize 2048 -keystore www.cheilsma.co.kr   
   
pw : tapaman   
   
What is your first and last name?   
  [Unknown]:  www.aa.co.kr   
What is the name of your organizational unit?   
  [Unknown]:  technology Lab       
What is the name of your organization?   
  [Unknown]:  aaron   
What is the name of your City or Locality?   
  [Unknown]:  dong-gu   
What is the name of your State or Province?   
  [Unknown]:  seoul     
What is the two-letter country code for this unit?   
  [Unknown]:  KR   
Is CN=www.aaron.co.kr, OU=technology Lab, O=tapacross, L=seongdong-gu, ST=seoul, C=KR correct?   
[no] : y   
   
   
   
Enter key password for <tapacross>   
        (RETURN if same as keystore password): Enter   
   
### 2. CSR 생성 및 확인 : keytool -certreq -alias aaron -file www.aaron.co.kr -keystore www.aaron.co.kr   
   
### 3. 확인 :    
[root@server179-149 ~]# more www.aaron.co.kr    
-----BEGIN NEW CERTIFICATE REQUEST-----   
MIICwzCCAasCAQAwfjELMAkGA1UEBhMCS1IxDjAMBgNVBAgTBXNlb3VsMRUwEwYDVQQHEwxzZW9u   
Z2RvbmctZ3UxEjAQBgNVBAoTCXRhcGFjcm9zczEXMBUGA1UECxMOdGVjaG5vbG9neSBMYWIxGzAZ   
BgNVBAMTEnd3dy5jaGVpbHNtYS5jby5rcjCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEB   
AMa1LytXu2ES6yAvqkYjErotLIPvUEIAA6NhhbAfc31JPggZD49E6h3O8I/Hc3gJ3Tiebradb1f+   
AvQqWqzTpQRwgXv92v0a3KWe1aG8S/ztPe2KWwGsT6wuvVZ1RH8w6zm8wpH0Xda4i5usIg8M22K0   
vJ0veWHIVVZGpHTqLKxlgtRPEKcY6IqOsLN+IXLXJ155lYXnssDsdIg95V5mLa9DelyENXPXpMSV   
o53RaOZDQwQmcw0JpW7wyJbWvnRojzZVinoY21zJiQEZy7sfNS5RZ0dwUnIMKBctI0MnN4kJFXpw   
lGWe7/hrUNX79y6yEsb23pZyN/31wKC91wwoVoMCAwEAAaAAMA0GCSqGSIb3DQEBBQUAA4IBAQA7   
X92ErVA8Soz7XXP4Y+GZg80JGWXTvkPKYInOU3Q/XrmvW15THnqJsWKInAqehKJE2dH+UoYlMaPJ   
***************************************************************   
/ML5I+nGrNf0UXXCkanz8W9BIDxTiqkBF0b1   
-----END NEW CERTIFICATE REQUEST-----   
   
   
디렉토리는 직접 만들어서 함   
/usr/csr   
   
   
