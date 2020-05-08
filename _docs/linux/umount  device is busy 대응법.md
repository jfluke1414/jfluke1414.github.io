---
order: 48
title: (LINUX) umount  device is busy 대응법
category: Linux
---

# fuser –cu 디렉토리
해당 디렉토리 사용자 또는 프로세스 확인
# fuser –ck 디렉토리
강제로 죽이기
이후 umount 실행


fuser -cu /Trendup20_Backup
fuser -ck /Trendup20_Backup
fuser -ck /Trendup20_DB
