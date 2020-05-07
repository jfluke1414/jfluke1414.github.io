---
order: 51
title: (ORACLE) Create oracle instance
category: Oracledb
---

--spfile***.ora 생성
/home/oracle/app/oracle/product/11.2.0/dbhome_1/dbs/spfileTEST.ora

-- .bash_profile 추가
export ORACLE_SID = TEST

--pfile 생성
create pfile='/home/oracle/app/oracle/product/11.2.0/dbhome_1/dbs/spfileTEST.ora' from spfile;
create pfile from spfile;


--nomount
startup nomount pfile='/home/oracle/app/oracle/product/11.2.0/dbhome_1/dbs/spfileTEST.ora';



1. listener.ora
   listener 추가

2. export ORACLE_SID 변경

2. sqlplus "/as sysdba"
startup




HJYEO =
  (DESCRIPTION =
    (ADDRESS = (PROTOCOL = TCP)(HOST = aa16)(PORT = 1521))
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = hjyeo)
    )
  )


LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
      (ADDRESS = (PROTOCOL = TCP)(HOST = test)(PORT = 1414))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = aa16)
      (ORACLE_HOME = /home/oracle/app/oracle/product/11.2.0/dbhome_1)
      (SID_NAME = orcl)
    )
  )


SID_LIST_LISTENER2 =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = aa16)
      (ORACLE_HOME = /home/oracle/app/oracle/product/11.2.0/dbhome_1)
      (SID_NAME = hjyeo)
    )
  )


imp rch20/tapaman@rch20 file=/rch20_Backup/20130608/rch20.dmp log=/rch20_Backup/rch20_imp.log full=y IGNORE=Y

create or replace directory db_backup as '/rch20_Backup';

--expdp
expdp rch20/tapaman@orcl DIRECTORY=db_backup tables=TB_ARTICLE_SEARCH_COMMUNITY DUMPFILE=TB_ARTICLE_SEARCH_COUMMINTY_expdp.dmp logfile=TB_ARTICLE_SEARCH_COUMMINTY_expdp.log

--impdp
impdp rch20/tapaman@rch20 directory=db_backup dumpfile=TB_ARTICLE_SEARCH_TWITTER_1201_expdp.dmp logfile=TB_ARTICLE_SEARCH_TWITTER_1201_impdp.log
