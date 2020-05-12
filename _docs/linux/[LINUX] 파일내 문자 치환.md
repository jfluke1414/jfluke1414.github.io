---
order: 94
title: (LINUX) [LINUX] 파일내 문자 치환
category: Linux
---

find /root/default.json -type f -exec sed -i 's/3002/80/g' {} \;

find /root/default.json -type f -exec sed -i 's/localhost/10.52.254.65:6502/g' {} \;