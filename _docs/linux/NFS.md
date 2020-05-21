---   
order: 47   
title: (LINUX) NFS   
category: Linux   
---   
   
### 1. 호스트 설정   
Vi /etc/hosts   
(연결할 상대방 IP 등록 서버와 클라이언트 모두)   
121.254.179.149         cheil_DB   
   
### 2. Export 설정   
Vi /etc/exports   
/backup   10.10.10.69(rw)(서버와 클라이언트 모두)   
(접속한 서버의 공유할 디렉토리) / 공유해줄 IP 주소(rw)   
   
### 3. Nfs 설정   
Cd /etc/rc.d/init.d   
./nfs restart(서버와 클라이언트 모두)   
   
### 4. 원격 붙을 클라이언트 서버에서 mount   
### 5. mount -t nfs 10.10.10.69:/disk02/trendup_anal /backup   
mount -t nfs 121.254.179.149:/disk01 /disk01/cheil_anal   
                 (붙을 서버 IP):/(서버 원격 공유 디렉토리 루트) /(현재 접속한 IP의 공유할 디렉토리 루트)   
