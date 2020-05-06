---
order: 28
title: Drop tablespace with missing datafile
category: Oracledb
---

Tablespace dbf 파일을 잘못 삭제했을경우

Today i have my new server installed with oracle 10G and i have to migrate old oracle 8i to this newly machine. I’ve already succeed mograting from oracle8i to oracle 10G by using export / import utility in oracle (later i will post how to do it in this blog)
Unfortunately i’m accidentally delete one datafile (not the system datafile) and when i want to shutdown the database i get this error code 
ORA-01157: cannot identify/lock data file 121 – see DBWR trace file
ORA-01110: data file 121: ‘/ora_data/ORADATA/USAGE_INDEX23_01.dbf’
to solve just do this simple step:
1.Shutdown abort your database to force shutdown
    sqlplus > shutdown abort
2.Startup mount database
 sqlplus > startup mount
3.After that issue this following command
sqlplus > ALTER DATABASE DATAFILE ‘<datafile name with complete path>’ OFFLINE DROP;
4.Then open the database
sqlplus > alter database open
5.Drop the tablespace by issue this following command
DROP TABLESPACE <tablespace name> INCLUDING CONTENTS;
6.After that if you have backup your database you can recover your tablespace.

----------------------------------------------------------------------------------
실제 명령순서대로 실행함.
1.DROP TABLESPACE "trendsrch20_33.dbf";
2.ALTER DATABASE DATAFILE '/ssd01/trendsrch20/trendsrch20_33.dbf' OFFLINE DROP;
3.alter database open
4.DROP TABLESPACE '/ssd01/trendsrch20/trendsrch20_33.dbf' INCLUDING CONTENTS;


