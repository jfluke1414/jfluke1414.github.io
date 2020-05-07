---
title: (ORACLE) DB start & stop
category: Oracledb
order: 3
---


ORACLE TELNET으로 접속하여
Sqlplus /nolog;

Conn sys as sysdba;

Password : dy15;

Shutdown immediate; (DB 내리기)

Startup;(DB 올리기)

Recover database until cancel;

Alter database open resetlogs;

Lsnrctl start;(Oracle Listener 시작) 

======================================================

1. DB 현상 파악 
   아래처럼 redo log 파일을 읽지 못하는 에러가 발생 
*
ERROR at line 1:
ORA-00313: open failed for members of log group 2 of thread 1
ORA-00312: online log 2 thread 1:
'/home/oracle/app/oracle/oradata/orcl/redo02.log'

2. mount만 하고 open 하지 않는다. 
SQL> startup mount;
ORACLE instance started.

Total System Global Area 1269366784 bytes
Fixed Size                  2144024 bytes
Variable Size             922749160 bytes
Database Buffers          335544320 bytes
Redo Buffers                8929280 bytes
Database mounted.

3. 복구 명령어 수행 
SQL> recover database until cancel;
Media recovery complete.
SQL> alter database open resetlogs;

4. oracle listener 시작 
lsnrctl start

