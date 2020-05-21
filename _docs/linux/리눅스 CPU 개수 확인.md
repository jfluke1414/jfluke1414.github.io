---   
order: 59   
title: (LINUX) 리눅스 CPU 개수 확인   
category: Linux   
---   
```   
물리 CPU 수   
grep "physical id" /proc/cpuinfo | sort -u | wc -l   
```
   
```
CPU당 물리 코어 수   
grep "cpu cores" /proc/cpuinfo | tail -1   
```