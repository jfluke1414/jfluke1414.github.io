---
order: 36
title: (LINUX) Web server 동시 접속자 수 알아내기
category: Linux
---

현재 접속 커넥션 수 알아내기
이 명령을 실제로 연결되어있는 커넥션 수를 알아내기에 적합합니다. 서버상에서 실제로 처리해야 하는 수를 의미합니다.
netstat -an | grep :80.*ESTABLISHED | wc -l

현재 접속 사용자(머신/디바이스) 수 알아내기
이 명령은 현재 동시 접속중인 사용자수를 알아내기에 적합합니다. 하나의 사용자가 동시에 여러개의 커넥션을 사용할 수 있는데 이것을 하나로 처리를 합니다.
netstat -an | grep :80.*ESTABLISHED | awk '{print $5}' | awk -F: '{print $1}' | sort | uniq | wc -l


모든 서비스 동시 접속자 수
netstat -nap | grep ESTABLISHED | wc -l
웹 동시 접속자 수
netstat -nap | grep :80 | grep ESTABLISHED | wc -l
웹 서버 커넷션 수
netstat -n|grep -F :80|egrep '(ESTAB|SYN)'|awk '{print $5}'|sed 's/:[0-9]*//'|sort -u|wc -l 
