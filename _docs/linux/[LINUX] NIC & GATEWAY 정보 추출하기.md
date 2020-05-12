---
order: 89
title: (LINUX) [LINUX] NIC & GATEWAY 정보 추출하기
category: Linux
---

The main NIC will usually have a default route. So:
ip -o -4 route show to default

The NIC:
ip -o -4 route show to default | awk '{print $5}'

The gateway:
ip -o -4 route show to default | awk '{print $3}'
