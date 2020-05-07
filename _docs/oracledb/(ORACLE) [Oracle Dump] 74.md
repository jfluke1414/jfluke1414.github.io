---
order: 29
title: (ORACLE) Oracle Dump 74
category: Oracledb
---

Backup.sh
export ORACLE_BASE=/oracle/app/oracle
export ORACLE_HOME=/oracle/app/oracle/product/11.2.0/dbhome_1
export ORACLE_SID=orcl
DATE=`date '+%Y%m%d'`
#backup up20
#rm -f /home/backup/*bak
#mv -f /home/backup/trendup20.dmp /home/backup/up20.dmp.bak


mkdir /backup/$DATE
/oracle/app/oracle/product/11.2.0/dbhome_1/bin/exp up20/aaman file=/backup/$DATE/up20_$DATE.dmp
 log=/backup/$DATE/up20_$DATE.log buffer=10240000

------------------------------------------------------------------------------

오라클 덤프하는 방법
 
1. 윈도우에서 실행
    1) 오라클 계정에 있는 데이터 exp
        ->exp 계정이름/비밀번호@서비스이름 file=경로 설정(예 : C:\testDUMP\oracleDUMP.dmp)
    2) 오라클 계정에 있는 테이블 데이터 exp
        ->exp 계정이름/비밀번호@서비스이름 tables=테이블이름 file=경로 설정(예 : C:\testDUMP\oracleDUMP.dmp)
 
2. 리눅스에서 실행
    1) 오라클 계정에 있는 데이터 exp
        ->exp 계정이름/비밀번호@서비스이름 file=경로 설정(예 : /.../.../.../testDUMP/oracleDUMP.dmp)
    2) 오라클 계정에 있는 테이블 데이터 exp
        ->exp 계정이름/비밀번호@서비스이름 tables=테이블이름 file=경로 설정(예 : /.../.../.../testDUMP/oracleDUMP.dmp)
 
오라클 덤프 인포트 하는 방법
※데이터를 인포트를 하지전에 계정이 있다면 계정을 삭제를 해주어야 한다.
 
1. 계정 및 테이즐 삭제
    1) 계정 삭제
        -> drop user 계정이름 cascade;
    2) 테이즐 삭제
        -> drop table 테이블 이름;
 
2. tablespace 생성, 계정생성, 권한주기
※각 유저별로 tablespace를 생성해주는게 좋습니다.
     1) 오라클 테이블 스페이스 만들기
          create tablespace [tablespace_name] 
          datafile '/home/oracle/oradata/DANBEE/[file_name].dbf' size 500m;

      2) 오라클 유저 만들기
          CREATE USER [user_name] 
         IDENTIFIED BY [password]
         DEFAULT TABLESPACE [tablespace_name]
         TEMPORARY TABLESPACE TEMP;

      3) 권한주기
           grant connect, dba, resource, EXP_FULL_DATABASE, IMP_FULL_DATABASE to [user_name];
 
3.윈도우에서 실행(도스창에서 실행)
    1) 계정에 있는 데이터 전체일경우
         -> exp에서 file경로로 이동
              예) C:\testDUMP>imp 계정이름/비밀번호@서비스이름 file=oracleDUMP.dmp full=Y
    2) 계정에 있는 테이블의 데이터일경우
         -> exp에서 file경로로 이동
               예) C:\testDUMP>imp 계정이름/비밀번호@서비스이름 tables=테이블이름 file=oracleDUMP.dmp
 
4. 리눅스에서 실행
     1) 계정에 있는 데이터 전체일경우
         -> exp에서 file경로로 이동
              예) /.../.../.../testDUMP>imp 계정이름/비밀번호@서비스이름 file=oracleDUMP.dmp full-Y
    2) 계정에 있는 테이블의 데이터일경우
         -> exp에서 file경로로 이동
               예) /.../.../.../testDUMP>imp 계정이름/비밀번호@서비스이름 tables=테이블이름 file=oracleDUMP.dmp 
