---
title: (ORACLE) Tablespace 생성
category: Oracledb
order: 21
---

-- 계정 생성 --
CREATE USER RCH20
IDENTIFIED BY aaman
DEFAULT TABLESPACE RCH20
TEMPORARY TABLESPACE TEMP;

--계정 권한 주기 --
GRANT connect, resource TO RCH20;
grant create session to RCH20;
grant dba to RCH20;


[오류 내용]
IMP-00013 : DBA만이 다른 DBA가 엑스포트한 파일을 임포트할 수 있습니다.
[처리 내용]
1. sql*plus로 접속한다(DBA role)
먼저 임포트 받을 계정으로 접속하고
conn /as sysdba로 접속한다
2. 임포트 받을 유저에게 아래 권한 부여
GRANT IMP_FULL_DATABASE TO USER;


 
/home/dbf/20_data 아래에 테이블 스페이스 생성
파일당 용량은 20480M
CREATE TABLESPACE "TRENDUP20_DATA" DATAFILE
'/ssd01/trendup20_data/trendup20_data_01.dbf' SIZE 20480M AUTOEXTEND OFF,
  '/ssd01/20_data/trendup20_data_02.dbf' SIZE 20480M AUTOEXTEND OFF,
  '/ssd01/20_data/trendup20_data_03.dbf' SIZE 20480M AUTOEXTEND OFF
LOGGING
ONLINE
PERMANENT
EXTENT MANAGEMENT LOCAL AUTOALLOCATE
BLOCKSIZE 8K
SEGMENT SPACE MANAGEMENT AUTO;
TEMP 와 UNDOTBS1 용량을 기존 DB 설정에 준하여 크기조정

기존 DB서버의 /home/backup/20.dmp 파일을 신규DB서버 20 계정으로 이관
연습.... -> 과정을 숙지
exp
imp
Exp

Export :
exp up20/aaman file=20.dmp log=up20.log full=y
Import :
imp up20/aaman file=20.dmp log=up20.log full=y ignore=y


 
SELECT resource_name, current_utilization, max_utilization, limit_value
FROM v$resource_limit; 
[oracle@db2 oracle]$ cd $ORACLE_HOME/dbs
[oracle@db2 dbs]$ pwd
/oracle/app/oracle/product/11.2.0/dbhome_1/dbs
