---   
order: 14   
title: (LINUX) setting linux network   
category: Linux   
---   
   
vi /etc/sysconfig/network-scripts/ifcfg-ens32   
BOOTPROTO=static   
IPADDR=192.168.5.161   
NETMASK=255.255.255.0   
NETWORK=192.168.5.0   
   
vi /etc/sysconfig/network   
HOSTNAME=localhost.localdomain   
GATEWAY=192.168.5.1   
   
systemctl restart network   
   
vi /etc/resolv.conf   
nameserver 8.8.8.8   
nameserver 8.8.4.4   
   
   
ifconfig를 이용한 ip 할당하는 방법   
#ifconfig eth0 down   
    
#ifconfig eth0 up   
   
#ifconfig eth0 192.168.0.100 netmask 255.255.255.255.0 broadcast 192.168.0.255 up   
   
