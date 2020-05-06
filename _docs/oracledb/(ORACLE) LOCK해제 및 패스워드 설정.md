---
order: 33
title: LOCK해제 및 패스워드 설정
category: Oracledb
---

[ORACLE]scott/tiger 계정에 대해서 LOCK해제 및 패스워드 설정

C:\>sqlplus "/as sysdba"

SQL> -- scott 계정의 LOCK을 해제
SQL> alter user scott account unlock;
사용자가 변경되었습니다.
SQL> -- soctt 계정의 패스워드를 tiger로 변경
SQL> alter user scott identified by tiger;
사용자가 변경되었습니다.
SQL> connect scott/tiger

연결되었습니다.



-- table space 생성--
CREATE TABLESPACE "BUZZDB16" DATAFILE
'/disk03/buzzdb16/tapa_data_01.dbf' SIZE 20480M AUTOEXTEND OFF,
'/disk03/buzzdb16/tapa_data_02.dbf' SIZE 20480M AUTOEXTEND OFF,
'/disk03/buzzdb16/tapa_data_03.dbf' SIZE 20480M AUTOEXTEND OFF,
'/disk03/buzzdb16/tapa_data_04.dbf' SIZE 20480M AUTOEXTEND OFF,
'/disk03/buzzdb16/tapa_data_05.dbf' SIZE 20480M AUTOEXTEND OFF

LOGGING
ONLINE
PERMANENT
EXTENT MANAGEMENT LOCAL AUTOALLOCATE
BLOCKSIZE 8K
SEGMENT SPACE MANAGEMENT AUTO;

-- 계정 생성 --
CREATE USER BUZZDB16
IDENTIFIED BY buzzdb16
DEFAULT TABLESPACE BUZZDB16
TEMPORARY TABLESPACE TEMP;

--계정 권한 주기 --
GRANT connect, resource TO BUZZDB16;
grant create session to BUZZDB16;
grant dba to buzzold;(table space 접근)



-- 락 현상 --
SELECT USERNAME, 
       ACCOUNT_STATUS,
           TO_CHAR(LOCK_DATE,'YYYY.MM.DD HH24:MI') LOCK_DATE           
FROM DBA_USERS
WHERE USERNAME = 'buzzdb16'

select * from all_users;


SELECT * FROM dba_users;


ALTER USER BUZZDB16 account unlock;

ALTER USER BUZZDB16 ACCOUNT LOCK;

ALTER USER BUZZDB16 IDENTIFIED BY tapaman12;

SELECT p.profile, p.resource_name, p.limit
  FROM dba_users u, dba_profiles p
  WHERE p.profile = u.profile
  AND username='BUZZDB16';
  
  
  SELECT U.USERNAME,P.PROFILE, P.RESOURCE_NAME, P.LIMIT 
FROM DBA_USERS U, DBA_PROFILES P 
WHERE P.PROFILE=U.PROFILE AND USERNAME='BUZZDB16';

BUZZDB16	DEFAULT	PASSWORD_VERIFY_FUNCTION	NULL

ALTER PROFILE DEFAULT limit PASSWORD_LOCK_TIME 1;

grant select on v_$lock to system


SELECT DISTINCT
         X.SESSION_ID,
         A.SERIAL#,
         D.OBJECT_NAME,
         A.MACHINE,
         A.TERMINAL,
         A.PROGRAM,
         A.LOGON_TIME,
         'alter system kill session ''' || A.SID || ',  ' || A.SERIAL# || ''';'
    FROM GV$LOCKED_OBJECT X, GV$SESSION A, DBA_OBJECTS D
   WHERE X.SESSION_ID = A.SID AND X.OBJECT_ID = D.OBJECT_ID
ORDER BY LOGON_TIME
