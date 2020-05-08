---
order: 26
title: (LINUX) 하나의 랜카드 2개 이상의 IP 할당하기 (가상IP)
category: Linux
---

#### 일단 현재 네트워크 정보가 어떻게 되어있는지 보자.
# cat /etc/sysconfig/network-scripts/ifcfg-eth0          

DEVICE=eth0
BOOTPROTO=static
BROADCAST=192.168.204.255
IPADDR=192.168.204.3
NETMASK=255.255.255.0
NETWORK=192.168.204.0
ONBOOT=yes

#### 가상 IP를 잡아 주기 위해서 네트워크 설정 파일을 그대로 복사하자
#### 이때 가상 네트워크를 잡을때는 ifcfg-eth0:[0-254] 로 255개 를 잡을 수 있다.
# cp /etc/sysconfig/network-scripts/ifcfg-eth0 /etc/sysconfig/network-scripts/ifcfg-eth0:0

#### 그런 후 추가한 파일을 열어서 DEVICE명과 IP를 변경해주자.
# vi /etc/sysconfig/network-scripts/ifcfg-eth0:0

DEVICE=eth0:0
BOOTPROTO=static
BROADCAST=192.168.204.255
IPADDR=192.168.204.43
NETMASK=255.255.255.0
NETWORK=192.168.204.0
ONBOOT=yes

#### 그런 후에 네트워크 데몬을 재실행시켜주자.
# /etc/rc.d/init.d/network restart
