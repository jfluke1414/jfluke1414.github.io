---
order: 54
title: (LINUX) directory structure
category: Linux
---

/ 

- 루트 디렉터리


/bin

- 기본적인 명령어가 저장된 디렉토리이다.
mv, cp, rm, rmdir, df, sync 등등.. 일반 계정 사용자도 사용하는 명령어 집합 디렉토리이다.

/boot

- 리눅스 부트로더 디렉토리. GRUB 와 같은 부트로더에 관한 파일들이 존재함.

/dev

- 시스템 디바이스(device)파일을 저장하고 있는 디렉토리. 하드디스크 장치파일 /dev/sda, 
CD-ROM 장치파일 /dev/cdrom 등.

/etc

- 시스템의 거의 모든 설정파일이 존재하는 디렉토리. 

/etc/passwd
/etc/group
yum 설정파일
xinetd 설정파일
vsftpd 설정파일
/etc/sysconfig (시스템 제어판용 설정파일)

/etc/mail/

- sendmail.cf 나 access 파일등의 sendmail의 설정파일들이 존재하는 디렉토리.

/etc/ssh/

- SSH 서비스, sshd 데몬에서 사용하는 설정파일들이 존재.

/etc/squid/

- squid 프락시서버 관련


/etc/samba/

- 삼바관련 설정파일

/etc/skel/

- 계정사용자 생성시 초기화파일들이 저장된 디렉토리. (useradd 에서 사용)

/etc/rc.d/

- 부팅레벨별 부팅스크립트 파일

/etc/rc.d/init.d/

- 시스템 초기화 파일들

/etc/pam.d/

- PAM 설정

/etc/httpd/

- RPM 으로 설치된 아파치 설정파일(httpd.conf 등)

/etc/cron.d/
/etc/cron.daily/
/etc/cron.hourly/
/etc/cron.monthly/
/etc/cron.weekly/

- 크론 설정파일

/etc/xinetd.d/

- xinetd 수퍼데몬에 의해 서비스되는 서비스 설정파일


/etc/yum/

- yum 설정관련 파일

/etc/sysconfig/

- 시스템 제어판 관련 파일


/home

- 사용자의 홈디렉토리.

/lib

- 커널모듈 파일과 라이브러리 파일.

/media

- DVD, CD-ROM, USB 장치등의 마운트포인트(mount point)로 사용되는 디렉토리


/mnt

- /media 디렉토리와 비슷한 용도로 사용되는 디렉토리

/proc 

- 가상파일 시스템. 현재 메모리에 존재하는 모든 작업들이 파일형태로 존재함.


/root

- root 사용자의 홈 디렉토리


/sbin

- ifconfig, e2fsck, ethtool, halt, shutdown 등.. 시스템 관리자용 명령어 디렉토리.


/usr

- 시스템이 아닌 일반 사용자들이 주로 사용하는 디렉토리.

/usr/bin/

- 일반 사용자들이 사용가능한 명령어 파일들이 존재하는 디렉토리.

/usr/X11R6/

- X 윈도우 시스템의 루트 디렉토리


/usr/include/

- C 프로그램 헤드파일 디렉토리


/usr/lib/

- /lib 에 들어가지 않은 라이브러리 디렉토리

/usr/sbin/

- /bin 에 제외된 명령어와 네트워크 관련 명령어가 들어있음.


/usr/src/

- 프로그램 소스

/usr/local/

- MYSQL, Apache, Proftpd, PHP 등 어플리케이션 소스로 컴파일설치할때 사용하는 장소


/usr/share/man/

- man 페이지 (manual page)

/var

- 시스템 운용중에 생성되었다가 삭제되는 데이터를 일시적으로 저장하기 위함 디렉토리.
거의 모든 시스템로그파일은  /var/log에 저장되고, DNS의  zone 설정파일은  /var/named 에 저장되고, 메일파일은  /var/spool/mail 에 저장되며, 크론설정파일은  /var/spool/cron 디렉토리에 각각 저장됨.

/var/tmp/

- /tmp 디렉토리와 같은 공용 디렉토리.

/var/log/

- 시스템로그파일 (messages, secure, xferlog ) 파일등이 저장되는 디렉토리.

/var/ftp/

- vsftp 등과 같은 FTP 서비스를 위한 다운로드될 파일들 즉, FTP 홈디렉토리


/var/named/

- BIND 즉, DNS 에서 사용하는 zone 파일들이 저장되는 디렉토리


/var/spool/mail/

- 각 계정 사용자들의 메일파일

  
/var/spool/lpd/

- 프린트를 하기 위한 임시 디렉토리


/var/spool/mqueue/

- 발송을 위한 메일 일시저장 디렉토리

/var/spool/cron/

- 각 사용자들의 cron 설정파일


/var/spool/at/

- atd 즉, 예약작업에 관한 파일들


/lost+found

- fsck 또는 e2fsck 등과 같은 파일시스템 체크 및 복구유틸리티 실행후에 주로 생성됨.
숫자 형태로 존재하는 파일의 내용을 확인후에, 파일명만 바꾸면 바로 복구 가능함.
