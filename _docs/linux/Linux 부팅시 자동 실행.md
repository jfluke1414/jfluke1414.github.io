---
order: 64
title: (LINUX) Linux 부팅시 자동 실행
category: Linux
---

리눅스 부팅시 자동실행(MS윈도우의 Autoexec.bat 과 같은 기능) 

예) # cd /etc/rc.d 

    # vi rc.local 

    ☞ 첫번째 명령 ; 두번째 명령 ==> ;(세미콜론)으로 구분한다. 

  
맨 아래 부분에 
cd /usr/local/mysql ; /bin/mysqld_safe & 
cd /usr/local/apache/bin ; ./apachectl start 


    # cd /root 
    # vi .bash_profile 


PATH=$PATH:$HOME/bin:/usr/local/mysql/bin  <= /usr/local/mysql/bin/ 을 추가한다. ( 간편하게 MySql 명령어 사용가능) 

또는 export PATH=$PATH:/usr/local/mysql/bin 을 추가한다.
 
