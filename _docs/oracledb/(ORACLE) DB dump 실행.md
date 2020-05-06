---
title: DB dump 실행
category: Oracledb
order: 5
---

1. 계정을 만든 후,
2. orange에서 계정의
DBA -> Space Manager -> Create TableSpace 
-> Table name 입력
TAPA_DATA
TAPA_INDEX

File size : 2048 Mbyte
Auto extend check
Max size : 1024 Mbyte

BigFile 선택

Enable logging
Don't generate redo logs, Not recoverable, Faster update 선택

3. Orcle@rsscrawler telnet에서
Import/dy15 root에서
./impdp.sh 실행


4. Impdp 파일을 수정해줘야 한다. 덤프파일 파일명을 적어주고 impdp 파일을 실행시킨다.

새로운 서버에서는 계정을 sys에서 계정을 만들어준다. (security Manager에서 계정 추가하면서 
Table space에서 해당하는 table space도 잡아준다.

