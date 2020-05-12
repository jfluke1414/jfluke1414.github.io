---
order: 87
title: (LINUX) [LINUX]ifconfig name 가져오기
category: Linux
---

Give this a try:
ifconfig -a | sed 's/[ \t].*//;/^$/d'
This will omit lo:

ifconfig -a | sed 's/[ \t].*//;/^\(lo\|\)$/d'

--------------------------------------------------------------
ip -o link show | awk -F': ' '{print $2}'
Or maybe:
ls /sys/class/net
