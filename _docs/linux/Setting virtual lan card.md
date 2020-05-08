---
order: 27
title: (LINUX) Setting virtual lan card
category: Linux
---

*. 리눅스 Network 설정

1. 랜카드 설정

명령어

랜카드 설정 및 설정정보 출력

ifconfig

ifconfig 인터페이스명 ip주소 [netmask] [broadcast] [up 또는 down]

ex)
[root@star ~]# ifconfig eth0:1 192.168.10.1 netmask 255.255.255.0 broadcast 192.168.10.255 up
[root@star ~]# ifconfig eth0:1
eth0:1 Link encap:Ethernet HWaddr 00:0C:29:9E:9E:DF
inet addr:192.168.10.1 Bcast:192.168.10.255 Mask:255.255.255.0
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
Interrupt:10 Base address:0x2000

*. netmask, braoadcast 값을 입력하지 않으면 디폴트 값이 적용된다.
*. up 을 붙이지 않더라도 fedora 에서는 up 이 된다.

랜카드 비활성화
[root@star ~]# ifconfig eth0:1 down
[root@star ~]# ifconfig eth0:1
eth0:1 Link encap:Ethernet HWaddr 00:0C:29:9E:9E:DF
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
Interrupt:10 Base address:0x2000

=> ip 설정값이 없어졌다.

*. 라우터 설정
설정값 보기.
[root@star ~]# route
Kernel IP routing table
Destination Gateway Genmask Flags Metric Ref Use Iface
192.168.37.0 * 255.255.255.0 U 0 0 0 eth0
169.254.0.0 * 255.255.0.0 U 0 0 0 eth0
default 192.168.37.2 0.0.0.0 UG 0 0 0 eth0
[root@star ~]#


라우터 설정정보 변경

default gateway 삭제

route delete default gw gw주소

ex)
[root@star ~]# route delete default gw 192.168.37.2
[root@star ~]# route
Kernel IP routing table
Destination Gateway Genmask Flags Metric Ref Use Iface
192.168.37.0 * 255.255.255.0 U 0 0 0 eth0
169.254.0.0 * 255.255.0.0 U 0 0 0 eth0
[root@star ~]#

default route 추가

route add default gw gw 주소

[root@star ~]# route add default gw 192.168.37.2
[root@star ~]# route
Kernel IP routing table
Destination Gateway Genmask Flags Metric Ref Use Iface
192.168.37.0 * 255.255.255.0 U 0 0 0 eth0
169.254.0.0 * 255.255.0.0 U 0 0 0 eth0
default 192.168.37.2 0.0.0.0 UG 0 0 0 eth0
[root@star ~]#

찾을 DNS 주소 지정

아래처럼 등록해 두면 된다.

[root@star ~]# cat /etc/resolv.conf
nameserver 168.126.63.1

영구설정

커맨드 라인에서 설정한 정보들은 메모리에만 남아 있는 상태이므로 리부팅하면 새로 설정해야 한다.
영구적으로 설정하려면 부팅시 자동으로 실행되는 네트워크 설정파일에 주소를 입력해야 한다.


ip 주소 설정파일
<PRE>
부팅하면 /etc/sysconfig/network-scripts 디렉토리에 있는 파일이 자동 실행된다.
아래와 같이 파일로 설정해두면 된다.

[root@star ~]# cat /etc/sysconfig/network-scripts/ifcfg-eth0
</PRE>
DEVICE=eth0
BOOTPROTO=none
BROADCAST=192.168.37.255
HWADDR=00:0C:29:9E:9E:DF
IPADDR=192.168.37.3
NETMASK=255.255.255.0
NETWORK=192.168.37.0
omBOOT=yes
TYPE=Ethernet
USERCTL=no
PEERDNS=yes
GATEWAY=192.168.37.2
IPV6INIT=no
[root@star ~]#

랜카드를 dhcp client 로 구성하는 경우에는 ifcfg-eth0 파일을 아래처럼 간단히 설정하면 된다.

DEVICE=eth0
omBOOT=yes
BOOTPROTO=dhcp

그리고 랜카드그 한장 더 있고 두번째 랜카드를 설정한다고 가정하면
파일명은 ifcfg-eth1 로 하고 파일안에 있는 DEVICE=eth1 이것만 다르고 나머지는
다 똑같은 방법으로 구성하면 된다.

*. 게이트웨이 주소는 /etc/sysconfig/network 파일에 기입해도 된다.

[root@star ~]# cat /etc/sysconfig/network
NETWORKING=yes
HOSTNAME=star
GATEWAY=192.168.37.2
[root@star ~]#

기타

/etc/hosts 파일은 host 이름과 ip 주소를 매핑하기 위한 파일이다.
여기에 등록되어 있는 host는 ip 대신 host 이름으로 접근할 수 있다.

[root@star ~]# cat /etc/hosts
# Do not remove the following line, or various programs
# that require network functionality will fail.
127.0.0.1 star localhost.localdomain localhost
[root@star ~]#

파일형식

host ip주소 host 이름 host이름에대한 alias1 host이름에 대한 alias2

*. alias 는 생략할수 있다.

네트워크 상태 확인 명령어

ping
nslookup
traceroute 등이 있다.

*. 가상 이더넷 인터페이스 장치(nic) 만들기
- 하나의 랜카드에 여러개의 ip를 부여할때 사용한다.

eth0 이 있으면 eth0:0 ~ eth0:255 사이의 장치를 만들수 있다.
eth1 이 있으면 eth1:0 ~ eth1:255 사이의 장치를 만들수 있다.

가상 nic 를 설정하는 방법은 장치명만 제외하면 실제장치를 구성하는것과 같다.

ex) ifconfig eth0:1 192.168.100.1 up

영구설정 역시 실제 nic 장치와 마찬가지로 /etc/sysconfig/netwokr-scripts/ifcfg-eth0:1 을 만들고 설정하면 된다.
