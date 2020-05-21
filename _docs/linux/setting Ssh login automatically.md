---   
order: 9   
title: (LINUX) setting Ssh login automatically.md   
category: Linux   
---   
   
### 접속할려는 서버에서    
   
1. Ssh-keygen -t rsa   
2. Enter, enter   
3. Ls -alh   
4. Cd .ssh   
5. Id_id_rsa_pub -> authorized_key 이름 변경   
6. Mv id_rsa.pub authorized_keys   
7. Chmod 600 id_rsa   
8. Chmod 600 authorized_keys   
9. 65번 서버에서 아래 실행   
10. scp authorized_keys snscrawler@**.**.**.**:/home/snscrawler/.ssh(접속할려는 서버 IP, .ssh 루트)   
