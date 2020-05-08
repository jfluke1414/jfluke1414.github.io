---
order: 24
title: (LINUX) Routing table Controll
category: Linux
---

route add -net 64.23.65.65 netmask 255.255.255.0 seth0
route del -net 64.23.65.65 netmask 255.255.255.0 seth0

route add -net 64.23.65.219 netmask 255.255.255.0 seth1
route del -net 64.23.65.219 netmask 255.255.255.0 seth1

route add -net 64.23.65.224 netmask 255.255.255.0 seth2
route del -net 64.23.65.224 netmask 255.255.255.0 seth2

route add -net 64.23.65.235 netmask 255.255.255.0 seth3
route del -net 64.23.65.235 netmask 255.255.255.0 seth3

route add -net 64.23.65.242 netmask 255.255.255.0 seth4
route del -net 64.23.65.242 netmask 255.255.255.0 seth4


Gateway defalut 설정
route del default gw 192.168.0.1 seth3
route add default gw 192.168.0.1 seth4

