---
order: 47
title: (ORACLE) Dump import table
category: Oracledb
---

1. 덤프하기(Export)
-기본
명령어프롬프트 > exp 아이디/비번@서비스명(SID)

-옵션(파일명 지정 또는 테이블 지정)
명령어프롬프트 > exp 아이디/비번@서비스명(SID)  tables=테이블명1,테이블명2...  file=파일명.dmp

2. 덤프파일 임포트 하기
-기본
명령어프롬프트 > imp 아이디/비번 file=파일명.dmp

-옵션 테이블지정
명령어프롬프트 > imp 아이디/비번 file=파일명.dmp tables=테이블명1,테이블명2...
덤프 넣을때 - import
D:\tmp>imp 아이디/비번
(일부 테이블만)
D:\tmp>imp 아이디/비번 file=파일명
tables=테이블명
/예)
exp test/testpw OWNER=test FILE=test.dmp LOG=test.log
exp test/testpw@test FILE=test.dmp LOG=test.log
imp test/testpw FROMUSER=test TOUSER=test FILE=test.dmp LOG = test.log

