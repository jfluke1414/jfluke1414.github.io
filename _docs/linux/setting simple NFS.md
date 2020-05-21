---   
order: 38   
title: (LINUX) setting simple NFS   
category: Linux   
---   
   
### 1. 데이타가 존재하는 서버에서..   
   
1) 아래 파일에서 공유할 디렉토리와 클라이언트IP를 등록합니다.   
   
# vi /etc/exports   
   
/nfsdata    192.168.0.100(rw,no_root_squash)   
   
※ /nfsdata : 공유할 폴더   
     192.168.0.100 : 접근 허용할 IP   
     rw,no_root_squash : read, write 권환과 해당 디렉토리에 대한 root 권한 할당. (옵션을 안주어도 됨)   
   
2) portmap 과 nfs 데몬이 실행중인지 확인 후, 실행이 되지 않았을 경우 가동시켜줍니다. (portmap 우선)   
   
# service portmap start  <- 반드시 nfs 시작 전에 구동해야함   
# service nfs start   
   
# rpcinfo -p  <- 열려있는 포트 확인 (열려있는 포트 모두 iptables에 등록 하고, 111, 2049는 udp 까지 등록 해줘야 한다)   
   
# vi /etc/sysconfig/nfs  <- 포트를 고정할 경우 아래항목 주석 해제   
   
RQUOTAD_PORT=875   
LOCKD_TCPPORT=32803   
LOCKD_UDPPORT=32769   
MOUNTD_PORT=892   
   
# rpcinfo -p  <- 열려있는 포트 재확인   
   
※ iptables 에서 관련포트를 모두 open 시켜 줍니다. (udp, tcp 모두 등록)   
    > 111, 875, 892, 2049, 32803, 32769   
※ nfs 가 없을경우, rpm이나 yum 으로 설치를 해줍니다.   
   
   
### 2. 클라이언트 서버에서..   
   
# service portmap start   
   
# mkdir /home/data_link (마운트하기전 디렉토리를 생성해준다.)   
   
# mount -t nfs -o nolock 192.168.0.99:/nfsdata /home/data_link   
   
부팅시에도 자동 마운트 되게 하고 싶을 경우, fstab 에 아래 항목을 등록해준다.   
   
# vi /etc/fstab   
   
ns:/nfsdata        /data_link    nfs    rw    0 0   
   
또는 /etc/rc.d/rc.local 에 mount 명령을 써넣어줘도 된다.   
   
[참고]   
/var/log/messages 에 아래와 같은 메세지가 반복 된다면..   
Oct 27 21:38:50 localhost kernel: statd: server localhost not responding, timed out   
Oct 27 21:38:50 localhost kernel: lockd: cannot monitor 192.168.0.100   
Oct 27 21:38:50 localhost kernel: lockd: failed to monitor 192.168.0.100   
    
mount 시 -o nolock옵션을 넣어보자.   
# mount -t nfs -o nolock 192.168.0.99:/nfsdata /home/data_link   
