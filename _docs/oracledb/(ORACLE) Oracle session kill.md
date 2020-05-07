---
title: (ORACLE) Oracle session kill
category: Oracledb
order: 15
---

ORA-00054 자원이 사용중이고 NOWAIT가 지정되어있습니다
란 오류를 만났을때..
TB에 락이 걸려있어 DML 혹은 DDL 사용시 저런 오류 메시지가 뜬다..
리모트 DB에서 insert 쿼리를 날렸는데 그 수행속도가 너무 느려 toad를 죽였다가 다시 살리니
아예 락이 걸려버린듯 하다 -_-;
DB를 restart 하는게 가장 좋은방법이지만 구글 형님과 네입훠 ~ 누님에게 물어보니 -_-;;
역시 해결책이 많더라..
1.  lock이 걸린 테이블이 DSD 라고 가정
SHELL> sqlplus system/manager
SQL> select a.sid, a.serial# from v$session a, v$lock b, dba_objects c
where a.sid=b.sid and b.id1=c.object_id and b.type='TM' and c.object_name='DSD';
SID  SERIAL#
---  --------
131  33324
2. 아래의 명령으로 session을 kill 시킨다
SQL> alter system kill session '131,33324';
3. kill 을 시켰는데도 ora-000031 을 내며 프로세스가 죽지않는경우
SQL> select   spid  from  v$process
where addr = (select paddr from v$session where sid = '131');
하면 실제 Unix에서의 SID가 나온다.
4. Unix명령어를 이용하여 Kill
SHELL> kill   -9   발견된 SPID
ex) kill  -9  567
인터넷에서 찾은자료들을 발췌하여 조합한것이다 ~ㅅ~
일단 참조를 위하여 메모..
