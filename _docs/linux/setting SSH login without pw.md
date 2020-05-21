---   
order: 8   
title: (LINUX) setting SSH login without pw   
category: Linux   
---   
   
상황 : B 클라이언트에서 일반계정(user1)으로 A 서버로 암호 없이 SSH 접속을 한다.   
B클라이언트 작업.   
### 1. user1 계정으로 접속 한다.   
   
### 2. ssh-keygen 명령으로 passphrase 에 암호를 입력하여 키를 생성한다.   
   
ssh-keygen -t rsa<엔터>   
Generating public/private rsa key pair.   
Enter file in which to save the key (/home/user1/.ssh/id_rsa):<엔터>    
Enter passphrase (empty for no passphrase): <암호입력>   
Enter same passphrase again: <암호입력>   
Your identification has been saved in /home/user1/.ssh/id_rsa.   
Your public key has been saved in /home/user1/.ssh/id_rsa.pub.   
The key fingerprint is:   
XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX user1@localhost.localdomain   
※ 암호는 입력해도 되고, 입력 없이 엔터 치시면 인증서 암호 따로 필요 없이 접근 됩니다.    
   
### 3. /home/user1/.ssh 폴더의 파일을 확인 후 id_rsa.pub 파일을 다운 받는다.   
합계 12   
-rw-------  1 user1 user 951  7월 25 15:03 id_rsa   
-rw-r--r--  1 user1 user 238  7월 25 15:03 id_rsa.pub   
-rw-r--r--  1 user1 user 669  7월 10 11:17 known_hosts   
   
   
### A서버 작업.   
### 1. A서버의 user1 아이디로 로그인 한다. (user1 뿐 아니라 다른 계정에서도 같은 작업을 하면, 그 계정으로 접근 됨.)   
### 2. /home/user1/.ssh/폴더로 접근하여 아까 다운 받은 id_rsa.pub 파일을 업로드 한 후, 파일 명을 authorized_keys로 변경 시킨 후, 권한을 600으로 변경한다.   
cat id_rsa.pub >> authorized_keys<엔터>   
chmod 600 authorized_keys<엔터>   
### B 클라이언트에서 확인   
### 1. B 클라이언트에 user1으로 접속하여 확인 한다.   
   
ssh user1@xxx.xxx.xxx.xxx   
Enter passphrase for key '/home/user1/.ssh/id_rsa': <암호 입력후 엔터(키 생성시 암호 입력을 안했다면 묻지 않고 바로 접속됨.)>   
