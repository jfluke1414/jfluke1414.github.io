---
order: 1
title: (Vmware) network setting - static
category: Vmware
---
```
vi /etc/sysconfig/network-scripts/ifcfg-ens32
BOOTPROTO=static
IPADDR=192.168.5.161
NETMASK=255.255.255.0
NETWORK=192.168.5.0

vi /etc/sysconfig/network
HOSTNAME=localhost.localdomain
GATEWAY=192.168.5.2
* setting gateway to 192.168.5.2(not 1)

vi /etc/resolv.conf
nameserver 8.8.8.8
nameserver 8.8.4.4

systemctl restart network

```