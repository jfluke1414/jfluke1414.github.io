---   
order: 43   
title: (LINUX) checking port number open   
category: Linux   
---   
   
#netstat -nap (열려 있는 모든 포트)   
#netstat -l 또는 netstat -nap | grep LISTEN (LISTEN 되는 모든 포트)   
#netstat -nap | grep ESTABLISHED | wc -l ( 모든 서비스 동시 접속자 수)   
#netstat -nap | grep :80 | grep ESTABLISHED | wc -l ( 웹 동시 접속자 수)   
   
   
### 포트스캔 명령어로 확인 하는 방법   
   
# TCP 포트 확인 방법   
nmap -sT -p 1-65535 localhost    
# UDP 포트 확인 방법   
nmap -sU -p 1-65535 localhost   
# 네트워크에 열린 포트 확인    
nmap -sX -p 22,53,110 211.239.111.*    
   
   
lsof 명령어로 확인 방법   
   
# 모든 네트워크 소켓 확인   
lsof -I   
