---   
order: 67   
title: (LINUX) Linux 내부 IP 설정   
category: Linux   
---   
   
Ifconfig eth* up   
Cd /etc/sysconfig/network-script/ifcfg-eth*    
Onboot yes   
   
ifconfig eth7 10.10.10.149 netmask 255.255.255.0 broadcast 10.10.10.255 up   
   
Routing table 추가   
route add -net 10.10.10.0 netmask 255.255.255.0 dev eth7   
