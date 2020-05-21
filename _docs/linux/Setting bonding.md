---   
order: 62   
title: (LINUX) Setting bonding   
category: Linux   
---   
   
CISCO(시스코)에서는 "Etherchannel", Sun에서는 "Trunking", 리눅스에서는 "Bonding"   
이라고 칭하는 여러개의 이더넷 어댑터를 하나로 묶어 네트워크 대역폭을 늘리고, 한개의   
이더넷이 죽었을경우 Redendency 할수있는 방법입니다.   
   
허브는 EtherChannel을 지원하는 스위치 가 필요하고, 리눅스 커널에서 Bonding 을지원   
이더넷 어댑터가 2개이상 필요합니다.    
   
같은 랜카드2개와 터널링지원 스위치가 필요하나 집에서 사용중인 SK21G 베어본의 내장   
PHY VIA VT6103, D-Link  DGE-530T PCI, 3COM 3C16791A 스위치, 페도라코어5 로   
Redendency를 구성해보겠습니다.   
   
### 1) 네트웍설정 확인   
   
ifconfig   
   
eth0      Link encap:Ethernet  HWaddr 00:30:1B:BB:xx:xx   
          inet6 addr: fe80::213:46ff:fe78:3fce/64 Scope:Link   
UP BROADCAST RUNNING SLAVE MULTICAST MTU:1500 Metric:1   
          RX packets:1526 errors:0 dropped:0 overruns:0 frame:0   
          TX packets:156 errors:0 dropped:0 overruns:0 carrier:0   
          collisions:0 txqueuelen:1000   
          RX bytes:132508 (129.4 KiB)  TX bytes:23797 (23.2 KiB)   
          Interrupt:18   
   
eth1      Link encap:Ethernet  HWaddr 00:13:46:78:xx:xx   
          inet6 addr: fe80::213:46ff:fe78:3fce/64 Scope:Link   
          UP BROADCAST RUNNING SLAVE MULTICAST  MTU:1500  Metric:1   
          RX packets:1540 errors:0 dropped:0 overruns:0 frame:0   
          TX packets:160 errors:0 dropped:0 overruns:0 carrier:0   
          collisions:0 txqueuelen:1000   
          RX bytes:127427 (124.4 KiB)  TX bytes:21098 (20.6 KiB)   
          Interrupt:19 Base address:0xc000   
   
   
### 2) /etc/modprobe.conf 수정   
   
alias bond0 bonding   <- 본딩모듈을 올려줍니다.   
alias eth0 via-rhine  <- VIA 내장 100M   
alias eth1 skge       <- 추가장착 D-Link  DGE-530T   
alias eth1 skgealias scsi_hostadapter sata_via   
alias scsi_hostadapter1 usb-storage   
   
   
### 2-1) /etc/sysconfig/network 파일   
   
NETWORKING=yes   
HOSTNAME=localhost.localdomain   
GATEWAY=192.168.0.1   
GATEDEV=bond0   
   
   
### 3) /etc/sysconfig/network-scripts/ 의 설정파일수정   
   
vim ifcfg-bond0 새로생성 (ifcfg-eth0 복사)   
   
DEVICE=bond0 <- 수정   
BOOTPROTO=static   
BROADCAST=192.168.10.255   
#HWADDR=00:30:1B:BB:xx:xx <-MAC 어드래스는 빼버립니다.   
IPADDR=192.168.10.4   
NETMASK=255.255.255.0   
ONBOOT=yes   
GATEWAY=192.168.10.1   
   
   
vim ifcfg-eth0   
   
# VIA Technologies, Inc. VT6102 [Rhine-II]   
DEVICE=eth0   
BOOTPROTO=none   
ONBOOT=yes   
MASTER=bond0   
SLAVE=yes   
TYPE=Ethernet   
   
   
vim ifcfg-eth1   
   
DEVICE=eth1   
ONBOOT=yes   
BOOTPROTO=none   
MASTER=bond0   
SLAVE=yes   
TYPE=Ethernet   
   
### 4) bond0 활성화    
   
  커널 2.6.XX   
/etc/modprobe.conf   
modprobe bonding   
## 위와같이 모듈을 인식시켜 줍니다.   
ifconfig eth0 up 0.0.0.0   
ifconfig eth1 up 0.0.0.0   
## 위 방법은 안될때 하는 방법입니다.    
   
ifup bond0 <- bond0 활성화   
   
ifenslave bond0 eth0 <- eth0 를 bond0 에 슬레이브   
ifenslave bond0 eth1 <- eth1 를 bond0 에 슬레이브   
   
혹은 /etc/rc.d/init.d/network restart 로 네트웍 디바이스들을 재시작해줍니다.   
   
ifconfig   
   
bond0     Link encap:Ethernet  HWaddr 00:13:46:78:xx:xx   
          inet addr:192.168.10.4  Bcast:192.168.10.255  Mask:255.255.255.0   
          inet6 addr: fe80::213:46ff:fe78:3fce/64 Scope:Link   
          UP BROADCAST RUNNING MASTER MULTICAST  MTU:1500  Metric:1   
          RX packets:5184302 errors:0 dropped:0 overruns:0 frame:0   
          TX packets:4937025 errors:0 dropped:0 overruns:0 carrier:0   
          collisions:0 txqueuelen:0   
          RX bytes:279838452 (266.8 MiB)  TX bytes:138131145 (131.7 MiB)   
   
eth0      Link encap:Ethernet  HWaddr 00:13:46:78:xx:xx   
          inet6 addr: fe80::213:46ff:fe78:3fce/64 Scope:Link   
          UP BROADCAST RUNNING SLAVE MULTICAST  MTU:1500  Metric:1   
          RX packets:1803934 errors:0 dropped:0 overruns:0 frame:0   
          TX packets:2468511 errors:0 dropped:0 overruns:0 carrier:0   
          collisions:0 txqueuelen:1000   
          RX bytes:2221561120 (2.0 GiB)  TX bytes:2224359808 (2.0 GiB)   
          Interrupt:19   
   
eth1      Link encap:Ethernet  HWaddr 00:13:46:78:xx:xx   
          inet6 addr: fe80::213:46ff:fe78:3fce/64 Scope:Link   
          UP BROADCAST RUNNING SLAVE MULTICAST  MTU:1500  Metric:1   
          RX packets:3380368 errors:0 dropped:0 overruns:0 frame:0   
          TX packets:2468517 errors:0 dropped:0 overruns:0 carrier:0   
          collisions:0 txqueuelen:1000   
          RX bytes:2353244628 (2.1 GiB)  TX bytes:2208739115 (2.0 GiB)   
          Interrupt:21 Base address:0x8000   
   
lo        Link encap:Local Loopback   
          inet addr:127.0.0.1  Mask:255.0.0.0   
          inet6 addr: ::1/128 Scope:Host   
          UP LOOPBACK RUNNING  MTU:16436  Metric:1   
          RX packets:30 errors:0 dropped:0 overruns:0 frame:0   
          TX packets:30 errors:0 dropped:0 overruns:0 carrier:0   
          collisions:0 txqueuelen:0   
          RX bytes:5690 (5.5 KiB)  TX bytes:5690 (5.5 KiB)   
   
