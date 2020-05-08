---
order: 29
title: (LINUX) Linux virtual lancard configuration away
category: Linux
---

ls
ifconfig eth0 down  <ip device 삭제>
ifconfig eth0 변경할 IP up  <ip device 추가>
ifconfig eth0:0 gateway up  < gateway 설정 >
route add default gw 192.168.10.1 eth0  < route defalut add>


ifconfig eth0 down
ifconfig eth0 192.168.10.30 up
ifconfig eth0:0 192.168.10.11 up
route add default gw 192.168.10.1 eth0

<Script 사용시>
#!/usr/bin/env bash

SERVERS=/home/cra/config/

while (true)
do
	for i in ` cat $SERVERS `
	do
		ifconfig eth0 down
		ifconfig eth0 $i up
		ifconfig eth0:0 ***.***.***.*** up
		route add default gw ***.***.***.*** eth0
		sleep 600
	done
done
