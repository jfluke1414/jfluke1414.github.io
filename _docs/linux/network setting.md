---      
order: 101      
title: (LINUX) network setting   
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
   
   
firewall 등록 안되어있을시(Minimal)   
yum install firewalld   
systemctl start firewalld.service   
   
[firewall]   
firewall-cmd --permanent --zone=public --add-port=80/tcp   
firewall-cmd --permanent --zone=public --add-port=6502/tcp   
   
firewall-cmd --permanent --zone=public --add-port=22/tcp   
firewall-cmd --permanent --zone=public --add-port=3306/tcp   
firewall-cmd --permanent --zone=public --add-port=3690/tcp   
   
* 허용한 포트 목록   
firewall-cmd --list-ports   
   
systemctl restart firewalld.service