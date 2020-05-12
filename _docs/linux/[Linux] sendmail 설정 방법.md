---
order: 73
title: (LINUX) [Linux] sendmail 설정 방법
category: Linux
---

1. sendmail이 서버에 존재하는지 확인.
(없으면 2번부서 시작, 설치되어 있으면 3번부터 시작)
rpm -qa | grep sendmail
 
2. yum으로 sendmail과 sendmail-cf 설치
yum -y install sendmail sendmail-cf
 
3. sendmail 실행
service sendmail start
 
설치 끝! 설정 시작~
 
cd /etc/mail
mv ./sendmail.cf sendmail.cf_old
cp ./sendmail.mc sendmail.mc_old
 
4. sendmail.mc 파일수정
52,53 line 수정 (앞부분 dnl 제거)
 
TRUST_AUTH_MECH(`EXTERNAL DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')dnl
define(`confAUTH_MECHANISMS', `EXTERNAL GSSAPI DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')dnl
 
 
 
116  line 수정
127.0.0.1을 0.0.0.0으로 개방
DAEMON_OPTIONS(`Port=smtp,Addr=127.0.0.1, Name=MTA')dnl
(수정 후)
DAEMON_OPTIONS(`Port=smtp,Addr=0.0.0.0, Name=MTA')dnl

5. m4 명령으로 sendmail.cf 생성
m4 sendmail.mc > sendmail.cf
생성확인~
-rw-r--r-- 1 root root 58697 Dec 26 16:30 sendmail.cf
-rw-r--r-- 1 root root 58691 Nov 27 09:29 sendmail.cf.bak
-rw-r--r-- 1 root root 58439 Nov 12  2010 sendmail.cf_old
-rw-r--r-- 1 root root 58691 Nov 27 09:43 sendmail.cf.rpmsave
-rw-r--r-- 1 root root  7192 Dec 26 16:19 sendmail.mc
-rw-r--r-- 1 root root  7202 Nov 28 08:38 sendmail.mc_old
-rw-r--r-- 1 root root  7192 Nov 27 09:41 sendmail.mc.rpmsave

6. sendmail.cf 수정
95line 수정(도메인이 있을 경우 수정. 없다면 크게 신경 안써도 됨)
# my official domain name
# ... define this only if sendmail cannot automatically determine your domain
#DjYour domian name


7. 445 line 보안을 위해 일부 글자 다음과 같이 삭제
O SmtpGreetingMessage=$j Sendmail $v/$Z; $b
(수정 후)
O SmtpGreetingMessage=$j Sendmail; $b


8. /etc/mail/local-host-names 도메인추가
*hostname과 local-host-names과 동일한 도메인 입력할것!
 
9. 서비스 재시작
 service sendmail restart
 
10. 테스트 메일 발송하기
# telnet localhost 25          // 방화벽에서 25번 포트를 열려있는지 확인할것. 안열려 있다면 방화벽에 막혀 메일전송 불가!
mail from:<me@mail.com>  //보내는 사람 주소
rcpt to:<you@mail.com>  //받는 사람 주소
data                        
hi. sendmail!!    //메일 내용 입력
.      //입력 마침. 내용작성 후 반드시 입력
 
quit   //종료
