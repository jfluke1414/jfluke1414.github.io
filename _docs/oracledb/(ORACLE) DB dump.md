---
title: (ORACLE) DB dump
category: Oracledb
order: 7
---

1. Oracle sysdb에서 계정을 만들고 해당 계정에서 space Manager에서
덤프를 받았던 DB의 table space와 같이 만들어준다.

2. Dump 받은 DB는 impdp.sh file vi impdp 에서 dump 할 file명을 적어주고 저장한다.

3. 그리고 나서 ./impdp.sh file을 실행하여 준다.
