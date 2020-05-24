---      
order: 1   
title: (Amazon) Amazon EC2 How to connect to instace from ssh tool   
category: Amazon      
---      
      
### Amazon EC2 How to connect to instace from ssh tool   
   
## 1. Amazon EC2 instance 만들때 kep pair 만들거나 만들었던거 선택   
 - .pem 파일을 저장   
   
## 2. putty gen 실행   
## 3. load pem 파일   
## 4. save   
putty 사용시 : save private file(ppk 파일명)   
ex> jfluke1313.ppk   
   
xshell 사용시   
export Openssh key   
ex> jfluke1313.ppk   
   
   
## 5. xshell 설정   
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
   
## 1. sudo passwd root   
setting pw   
   
## 2. su - root   
   
