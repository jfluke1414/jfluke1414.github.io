---
order: 58
title: (LINUX) setting Shmmax, shmall
category: Linux
---

110719476736



echo 110719476736 > /proc/sys/kernel/shmmax
echo 110719476736 > /proc/sys/kernel/shmall

echo “kernel.shmmax = 2147483648” >> /etc/sysctl.conf
echo “kernel.shmall = 2147483648” >> /etc/sysctl.conf
