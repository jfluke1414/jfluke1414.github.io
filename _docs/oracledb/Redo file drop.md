---
order: 49
title: Redo file drop
category: Oracledb
---

select file#,status,name from rch20;


alter database drop logfile '/oracle/app/oracle/oradata/rch20/redo01.log'; 
alter database drop logfile '/oracle/app/oracle/oradata/rch20/redo02.log'; 
alter database drop logfile '/oracle/app/oracle/oradata/rch20/redo03.log'; 