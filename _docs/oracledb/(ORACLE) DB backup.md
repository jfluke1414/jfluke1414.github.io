---
title: DB backup
category: Oracledb
order: 6
---

Dy15 계정에서 새로운 계정을 만들어
DBA -> security Manager -> create user -> 
Default tablespace -> TAPA_DATA
Temporary table space -> TEMP

Roles Granted -> 


Create table backup.syndi-soureces as (select *
From syndi-sources)
