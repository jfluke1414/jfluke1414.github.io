---
order: 27
title: (ORACLE) TableSpace 상태 점검
category: Oracledb
---

TabelSpace 상태를 점검한다.


SELECT
  ts.status
 ,data.name
 ,ts.contents
 ,extent_management
 ,data.Mbytes "SPACE(MB)"
 ,free.free   "FREE(MB)"
 ,trunc((data.Mbytes-free.free)/data.Mbytes*100,2) "Used(%)"
FROM ( select 
     tablespace_name name
    ,trunc(sum(bytes/1024/1024)) Mbytes
   from dba_data_files
         group by tablespace_name
     ) data,
  ( select 
      free.tablespace_name
     ,trunc(sum(free.bytes)/1024/1024,1) free
   from dba_free_space free
  group by free.tablespace_name
  ) free,
dba_tablespaces ts
WHERE data.name = free.tablespace_name
  AND data.name = ts.tablespace_name
;
