---
order: 88
title: (LINUX) [LINUX] CentOS 7 타임존 변경
category: Linux
---

CentOS 7 에서 타임존 변경 방법입니다.

사용가능한 타임존
# timedatectl list-timezones | grep Seoul
Asia/Seoul

타임존 변경
# timedatectl set-timezone Asia/Seoul

수동으로 변경해야 할 경우는 기존의 /etc/localtime 파일을 삭제 후
# ln -s /usr/share/zoneinfo/Asia/Seoul /etc/localtime

타임존 확인
# date
2016. 01. 18. (월) 21:12:30 KST
