---   
order: 30   
title: (LINUX) ifconfig.sh   
category: Linux   
---   
```   
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
```