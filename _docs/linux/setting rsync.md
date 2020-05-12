---
order: 56
title: (LINUX) setting rsync
category: Linux
---

1. 서버 쪽 (마스터)
 
[root@doom1 ~]# rpm -qa | grep rsync     // rsync 설치 확인
rsync-2.6.8-3.1
[root@doom1 ~]# vi /etc/xinetd.d/rsync    // rsync를 xinetd를 이용하여 실행시키기 위해 /etc/xinetd.d/rsync 파일을 수정
# default: off
# description: The rsync server is a good addition to an ftp server, as it \
#       allows crc checksumming etc.
service rsync
{
        disable = no
        socket_type     = stream
        wait            = no

        user            = root
        server          = /usr/bin/rsync
        server_args     = --daemon
        log_on_failure  += USERID
}
[root@doom1 ~]# vi /etc/rsyncd.conf      // 설정파일 생성
[aporia]     -----> 서비스명
path = /disk01/data_contents
comment = webservice-dir
uid = root
gid = root
use chroot = yes
read only = yes
hosts allow = 210.114.***.209     -----> 허락할 ip주소
max connections = 1
timeout = 300
 
[root@doom1 ~]# /etc/rc.d/init.d/xinetd restart       //xinetd 재가동
 
[root@doom1 ~]#telnet localhost 873        // 873포트 오픈 확인
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
@RSYNCD: 26
Localhost rsync server
sysadmin = root@localhost.com
 
 
 
2. 클라이언트쪽 (백업서버)
 
사용법 : rsync -avzrt hostname(IP)::서비스명 백업디렉토리
예제> rsync -avzrt 210.1gre14.***.208::aporia /home/
 
rsync 옵션
-a : archive mode 심볼릭 링크, 속성, 퍼미션, 소유권등을 보존한다.
-v : verbose 진행상황을 상세하게 보여준다.
-z : compress 전송시 압축을 수행한다.
-r recursive (하위 디렉토리까지 포함)
-t 변경시간 전송 (이것이 없으면 전송한 시간으로 바뀜)
-u : update only 새로운 파일을 덮어쓰지 않는다.
-e : 복사를 위한 원격접속쉘 프로그램을 설정한다.
--delete : 서버측에 없고 클라이언트측에만 있는 파일을 지운다

