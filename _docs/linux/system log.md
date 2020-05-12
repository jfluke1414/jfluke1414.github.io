---
order: 76
title: (LINUX) system log
category: Linux
---

로그이름	로그파일명	관련데몬	설명
커널로그	/dev/console	 	콘솔에 뿌려지는 로그
시스템로그	/var/log/messages	syslogd	리눅스커널로그 및 주된로그
보안로그	/var/log/secure	inetd	inetd에 의한 로그
메일로그	/var/log/maillog	sendmail	메일로그(sendmail에 의한 로그)
		popper
크론로그	/var/log/cron	crond	crond에 의한 로그
부팅로그	/var/log/boot.log	 	시스템부팅시의 로그
FTP로그	/var/log/xferlog	ftpd	ftp로그
웹로그	/usr/local/apache/logs/access_log	httpd	아파치(웹서버)로그
네임서버로그	/var/log/named.log	named	네임서버(DNS)로그
