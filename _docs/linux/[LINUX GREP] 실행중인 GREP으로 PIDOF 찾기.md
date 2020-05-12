---
order: 98
title: (LINUX) [LINUX GREP] 실행중인 GREP으로 PIDOF 찾기
category: Linux
---

ps -ef | grep node |grep -v grep | awk '{print $2}'