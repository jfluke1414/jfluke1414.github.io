---
title: Oracle Merge into
category: Oracledb
order: 9
---

MERGE INTO의 목적은 어떤 테이블이나 뷰테이블을 해당 목표테이블과 합체(MERGE)하기 위한 목적인데요. 이걸 이용해서 데이터가 들어왔을 때 있는 데이터면 UPDATE하고, 없는 데이터면 INSERT하는 형태로도 쓰일 수 있습니다. 

http://radiocom.kunsan.ac.kr/lecture/oracle/sql/merge.html
위에는 MERGE INTO를 잘 설명한 사이트네요.

여기서 조금 응용하면 원하는 대로 구현할 수 있습니다-_-;

MERGE INTO 테이블명  별칭
USING 대상테이블/뷰  별칭
ON 조인조건
WHEN MATCHED THEN
  UPDATE SET
   컬럼1=값1
   컬럼2=값2
WHEN NOT MATCHED THEN
  INSERT (컬럼1,컬럼2,...)
       VALUES(값1,값2,...);
MERGE INTO다음에 나오는 테이블명은 실제로 데이터가 들어가거나 업데이트 되는 테이블이구요.
USING 다음에 나오는 테이블명은 실제 데이터를 가져오거나 할 테이블이구요.
ON은 WHERE과 같은 조건문이죠. 
WHEN MATCHED THEN은 매치되는게 있으면 UPDATE하라는 얘기구요.
WHEN NOT MATCHED THEN은 매치되는게 없으면 INSERT하게 되죠.

응용해봅시다.
[code]
           MERGE INTO INSERTTABLE
           USING DUAL
           ON (ID = 1)
           WHEN MATCHED THEN
           UPDATE SET
           DATA = 'idoori'
           WHEN NOT MATCHED THEN
           INSERT (ID, DATA)
           VALUES (1, 'mudchobo')
[/code]
INSERTTABLE이라는 곳에 USING은 DUAL이라고 했는데 DUAL은 dual은 1개의 레코드 만을 갖는 dummy 테이블이라고 합니다. select 1 from dual해버리면, 1이 나오죠. 대상테이블은 필요없으니 dual로 설정합니다.
ON에서 ID = 1은 ID가 1인게 만약 있으면, DATA부분을 idoori로 업데이트하고, 없으면 mudchobo로 넣게 되는겁니다.  


