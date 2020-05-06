---
order: 46
title: Full Undo table space
category: Oracledb
---

select * from v$parameter
where name like '%undo_retention%';
-- default : 900(second)
-- not support : LOB
-- GF : 3600(sec) -> 60 min

flashback 관련 해서 undo_retention 사이즈, undo tablespace 사이즈 를 조절하려고하는데...
아래 자료는 네이버에서 찾은 자료인데... 보통 사이즈를 어떻게 산정하시는지 궁금합니다.
 
1) undo_retention 사이즈
 => 아래 쿼리에서 나온 값보다는 커야한다면 얼마나 더 큰값으로 하는게 적정값인지 궁금합니다.
 
 
SQL> select max(maxquerylen) from v$undostat;
MAX(MAXQUERYLEN)
----------------
210
v$undostat의 maxquerylen 칼럼은 하루동안 수행된 가장 긴 transaction 크기(초)를 의미한다. Undo retention parameter는 위 칼럼의 값보다 최소한 커야 할 것이다.
 
 
 
2) undo tablespace 사이즈
=> 아래의 방법대로 계산하여 나온값으로 하는것이 제대로 된 방법인가요??
 
 
[Undo tablespace 크기 계산 방법]
undo tablespace의 크기를 계산 하기 위하여 아래의 세가지 정보가 필요하다.
- undo retention 시간(UR) ?
- 초당 발생하는 undo block의 수(UPS) ?
- 확장 영역 및 파일 크기에 따라 달라지는 overhead(DBS) ?
 
Undo tablespace 크기 산정 공식 = (UR*UPS*DBS)+(DBS*24)
 
위 세가지 정보 중 초당 발생하는 undo block의 수는 v$undostat view에서 확인 가능하다.
SQL>select (sum(undoblks)/sum((end_time-begin_time)*86400)) from v$undostat;
 
위 세가지 정보를 이용하여 아래의 query를 사용하여 undo tablespace크기를 계산할 수 있다.
SQL>Select (UR*UPS*DBS)+(DBS*24) AS "bytes"
From (select value AS UR from v$parameter where name='undo_retention'),
(select (sum(undoblks)/sum(((end_time-begin_time)*86400))) AS UPS
from v$undostat),
(select value AS DBS from v$parameter where name='db_block_size'); 

--------------------------------------------------------
1. undo_retention
commit 된 정보에 대해서도 undo 이미지를 유지하기 위한 시간.
이것이 가능하게 됨으로써 9i 버전이후에 flashback 사용이나, long query 시 ORA-01555 를 최소화하는 것이 가능하게 되었습니다.
*. expired extent : undo_retention 시간을 초과한 extent. transaction이 commit 된 후 undo image가 undo_retention 시간을 초과한 경우.
*. unexpired extent : undo_retention 시간을 최과하지 않은 extent. 
undo tablespace의 공간이 충분하다면 oracle 이 commit 된 정보에 대해서 가능하면 오랫동안 유지하는 방향으로 extent를 할당하게 됩니다.
이로인해 undo tablespace의 free space를 조회해 보면 항상 100% 사용된 것으로 보여지는 경우가 있습니다.

select status, sum(bytes), count(*)
from dba_undo_extents
group by status;
10gR2 부터는 고정 undo tablespace(datafile autoextensible NO)에 대해서 undo guarantee mode가 아니면, undo_retention parameter는 무시되며, 
undo tablespace의 크기와 사용량에 의해서 undo retention값을 최대값으로 자동으로 설정한다.

