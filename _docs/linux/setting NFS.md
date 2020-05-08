---
order: 37
title: (LINUX) setting NFS
category: Linux
---

서버측 설정

portmap과 NFS를 실행해야 합니다. 그리고 nsflock도 실행해주세요.

설치가 되어있지 않다면 설치해주세요. 

CentOS는 기본적으로 설치가 되어있으니 설치과정은 넘어갑니다.


# /etc/init.d/portmap start
portmap (을)를 시작 중: [  OK  ]

# /etc/init.d/nfs start
NFS 서비스를 시작 중:  [  OK  ]
NFS 쿼터를 시작 중: [  OK  ]
NFS 데몬을 시작 중: [  OK  ]
NFS mountd를 시작 중: [  OK  ]

# /etc/init.d/nfslock start




# rpcinfo -p

로 확인하면 아래와 같이 포트번호와 사용중인 목록이 나옵니다.

nfs랑 portmap이 보이면 잘 실행되고 있는것 입니다.

100000    2   tcp    111  portmapper
100000    2   udp    111  portmapper
100011    1   udp    625  rquotad
100011    2   udp    625  rquotad
100011    1   tcp    628  rquotad
100011    2   tcp    628  rquotad
100003    2   udp   2049  nfs
100003    3   udp   2049  nfs
100003    4   udp   2049  nfs
100021    1   udp  54868  nlockmgr
100021    3   udp  54868  nlockmgr
100021    4   udp  54868  nlockmgr
100003    2   tcp   2049  nfs
100003    3   tcp   2049  nfs
100003    4   tcp   2049  nfs
100021    1   tcp  36016  nlockmgr
100021    3   tcp  36016  nlockmgr
100021    4   tcp  36016  nlockmgr
100005    1   udp    654  mountd
100005    1   tcp    657  mountd
100005    2   udp    654  mountd
100005    2   tcp    657  mountd
100005    3   udp    654  mountd
100005    3   tcp    657  mountd



마운트할 디렉토리를 설정하기 위해 /etc/exports 파일을 열어 아래의 내용을 추가합니다.


# vi /etc/exports
/home/nfs 192.168.5.123(rw)


/home/nfs 폴더에 대해서 192.168.5.123 아이피에 rw(읽기쓰기)권한을 준다는 설정입니다.

nfs 재실행합니다.


# /etc/init.d/nfs restart
NFS mountd를 종료 중: [  OK  ]
NFS 데몬을 종료 중: [  OK  ]
NFS quota를 종료 중: [  OK  ]
NFS 서비스를 종료 중:  [  OK  ]
NFS 서비스를 시작 중:  [  OK  ]
NFS 쿼터를 시작 중: [  OK  ]
NFS 데몬을 시작 중: [  OK  ]
NFS mountd를 시작 중: [  OK  ]


서버측 설정이 끝났습니다.


NSF 설정을 확인하고자 할때는

# showmount -e

이 명령어로 확인이 가능합니다.

------------------------------------------------------------------------------------------------

클라이언트측


portmap과 nfs를 실행합니다. 



# /etc/init.d/portmap start
portmap (을)를 시작 중: [  OK  ]

# /etc/init.d/nfs start
NFS 서비스를 시작 중:  [  OK  ]
NFS 쿼터를 시작 중: [  OK  ]
NFS 데몬을 시작 중: [  OK  ]
NFS mountd를 시작 중: [  OK  ]



마운트를 실행합니다
 
# mount -t nfs 192.168.5.123:/home/nfs /home/nfs


192.168.5.123서버의 /home/nfs 폴더를 /home/nfs 폴더에 마운트 하는 명령어 입니다.

명령이 잘 실행되었다면 NFS설정이 완료된 것입니다.



마운트한 폴더를 삭제할때는 먼저 마운트를 해제해주세요.

# umount /home/nfs




서버나 클라이언트 쪽에서 부팅시 자동으로 올라오도록 설정하기 위해서는 아래의 명령어를 실행하면 됩니다.

# chkconfig --level 3 nfs on
# chkconfig --level 3 portmap on




여기까진 어렵지 않은데 방화벽이 있을경우가 설정이 복잡해집니다.

NFS 사용할때 랜덤방식으로 포트번호가 변경되기 때문에 포트를 고정시켜주는 작업이 필요하고

이 고정된 포트에 대해서 방화벽을 해제해주셔야 합니다.

서버측에서 방화벽이 있는 경우 아래의 작업을 추가로 진행해주어야 합니다.


# rpcinfo -p

로 사용중인 포트를 다시 확인해봅시다.

100000    2   tcp    111  portmapper
100000    2   udp    111  portmapper
100011    1   udp    625  rquotad
100011    2   udp    625  rquotad
100011    1   tcp    628  rquotad
100011    2   tcp    628  rquotad
100003    2   udp   2049  nfs
100003    3   udp   2049  nfs
100003    4   udp   2049  nfs
100021    1   udp  54868  nlockmgr
100021    3   udp  54868  nlockmgr
100021    4   udp  54868  nlockmgr
100003    2   tcp   2049  nfs
100003    3   tcp   2049  nfs
100003    4   tcp   2049  nfs
100021    1   tcp  36016  nlockmgr
100021    3   tcp  36016  nlockmgr
100021    4   tcp  36016  nlockmgr
100005    1   udp    654  mountd
100005    1   tcp    657  mountd
100005    2   udp    654  mountd
100005    2   tcp    657  mountd
100005    3   udp    654  mountd
100005    3   tcp    657  mountd


111 포트와 2049번 포트를 제외하고 나머지 포트는 NFS가 실행될때마다 변경되는데요 포트를 고정시켜야 합니다.


# vi /etc/init.d/nfslock

start() {
    if [ ! -f /var/lock/subsys/nfslock ]; then
        # Start daemons.
        if [ "$USERLAND_LOCKD" ]; then
          echo -n $"Starting NFS locking: "
          daemon rpc.lockd -p 4000


/etc/init.d/nfslock을 열어 daemon rpc.lockd -p 4000 로 수정해주세요.


# vi /etc/sysconfig/nfs
LOCKD_TCPPORT=4001
LOCKD_UDPPORT=4001
MOUNTD_PORT=4002

/etc/sysconfig/nfs에서 TCP, UDP, MOUNTD 포트번호를 고정합니다.



# vi /etc/services


# pxc-splr-ft  4003/tcp                   # pxc-splr-ft
# pxc-splr-ft 4003/udp                   # pxc-splr-ft
rquotad         4003/tcp                        # rpc.rquotad tcp port
rquotad         4003/udp                        # rpc.rquotad udp port



/etc/services를 열어 4003번 포트에 대한 내용을 추가해야합니다. 기존 4003번 포트는 주석처리해주세요.

자 이제 수정한 값을 적용하기 위해 NFS를 재실행합니다.


# /etc/rc.d/init.d/nfslock restart
# /etc/rc.d/init.d/nfs restart


포트가 잘 변경되었는지 확인해봅시다.



# rpcinfo -p
100000    2   tcp    111  portmapper
100000    2   udp    111  portmapper
100024    1   udp    614  status
100024    1   tcp    617  status
100011    1   udp    668  rquotad
100011    2   udp    668  rquotad
100011    1   tcp    671  rquotad
100011    2   tcp    671  rquotad
100003    2   udp   2049  nfs
100003    3   udp   2049  nfs
100003    4   udp   2049  nfs
100003    2   tcp   2049  nfs
100003    3   tcp   2049  nfs
100003    4   tcp   2049  nfs
100021    1   udp   4001  nlockmgr
100021    3   udp   4001  nlockmgr
100021    4   udp   4001  nlockmgr
100021    1   tcp   4001  nlockmgr
100021    3   tcp   4001  nlockmgr
100021    4   tcp   4001  nlockmgr
100005    1   udp   4002  mountd
100005    1   tcp   4002  mountd
100005    2   udp   4002  mountd
100005    2   tcp   4002  mountd
100005    3   udp   4002  mountd
100005    3   tcp   4002  mountd


4001번 4002번 포트를 잘 사용하고 있네요.

이제 NFS에 사용되는 포트들에 대해서 방화벽을 해제합니다.


# vi /etc/sysconfig/iptables
-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 111 -j ACCEPT
-A RH-Firewall-1-INPUT -m state --state NEW -m udp -p udp --dport 111 -j ACCEPT
-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 2049 -j ACCEPT
-A RH-Firewall-1-INPUT -m state --state NEW -m udp -p udp --dport 2049 -j ACCEPT
-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 4000:4004 -j ACCEPT
-A RH-Firewall-1-INPUT -m state --state NEW -m udp -p udp --dport 4000:4004 -j ACCEPT


그리고 iptables를 재실행합니다.
 
# /etc/rc.d/init.d/iptables restart




서버측의 hosts.allow 또는 hosts.deny에 클라이언트측 서버에 대한 접근을 허용 또는 막아놓았다면 이에 대한 허용처리도 해주어야 합니다.


# vi /etc/hosts.allow
portmap : 192.168.5.123
mountd : 192.168.5.123



nfs가 실행이 되지 않았거나, 방화벽이 열리지 않았거나, host가 막혀있다면

authentication error
RPC Error: Program not registered.

클라이언트측에서 mount 명령어를 실행할때 이런 종류의 에러메시지를 받을 수 있습니다.

이런 메시지가 나타난다면, 서버측과 클라이언트 측의 nfs 관련 서비스가 잘 실행되고 있는지 확인해주시고,

방화벽이나 특정 ip에 대해서 접근을 막아놓지 않았는지 확인해보세요.

구글링을 통해 보니 이런 오류메시지가 나왔을때

다른 분들의 경험에서는 hosts.allow, hosts.deny파일의 퍼미션이 604이상이 되어야 한다고도 하네요.
