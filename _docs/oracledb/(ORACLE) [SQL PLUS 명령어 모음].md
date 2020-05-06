---
order: 32
title: [SQL PLUS 명령어 모음]
category: Oracledb
---

데이터베이스 시작하기
SQL> STARTUP
단계별로 시작하기
SQL> STARTUP NOMOUNT; //NOMOUNT 단계
SQL> ALTER DATABASE MOUNT; //MOUNT 단계
SQL> ALTER DATABASE OPEN; //OPEN 단계
옵션 사용하여 시작하기
SQL> STARTUP RESTRICT; //OPEN 단계까지 구동. 일반 사용자 사용 금지
SQL> STARTUP FORCE; //자동 종료 후 다시 시작
SQL> STARTUP PFILE; //파라미터 파일을 별도로 설정
SQL> STARTUP EXCLUSIVE MOUNT; //마운트 상태로 시작. 일반 사용자 접속 금지
시작 후 몇 가지 실행
RESTRICT 사용하여 시작하였을 때 모든 사용자가 접근할 수 있게 변경하기
SQL> ALTER SYSTEM DISABLE RESTRICTED SESSION;
메모리 영역 확인으로 정상 구동 여부 확인하기
SQL> show sga
생성되어 있는 사용자 확인하기
SQL> SELECT * FROM ALL_USERS;
자료사전 테이블 조회하기
SQL> SELECT * FROM V$SGA; //메모리 영역 정보 참조
SQL> SHOW SGA; //메모리 영역 정보 참조
SQL> SELECT * FORM V$PARAMETER; //DB 환경 정보 참조
SQL> SHOW PARAMETER; //DB 환경 정보 참조
SQL> SELECT * FROM DBA_USERS; //일반적인 자료 사전. 오픈 단계가 되어야 사용 가능
※ SYS 사용자와 SYSTEM 사용자가 만든 테이블을 자료사전(Data Dictionary)라고 한다.
종료
종료하기
SQL> shutdown normal //CLOSE단계->DISMOUNT단계->DISCONNECT단계. 사용자 접속 해제(disconnect)까지 기다렸다가 종료
SQL> shutdown //normal 옵션 사용과 동일
옵션과 함께 종료하기
SQL> SHUTDOWN TRANSACTINAL //사용자가 트랜잭션 종료까지 기다렸다가 종료
SQL> SHUTDOWN IMMEDIATE //즉시 종료. 사용자 존재 시 모든 트랜잭션은 롤백된다
SQL> SHUTDOWN ABORT //트랜잭션 롤백하지 않고 즉시 강제 종료. 정전 발생 시와 같다. 백업과 복구 작업 시에나 사용
top
SQL*PLUS 명령어
SQL*PLUS 실행 명령어
SQL> / //SQL문 또는 PL/SQL 블록을 실행한다
SQL> RUN //SQL문 또는 PL/SQL 블록을 실행한다
SQL> HELP //SQL, PL/SQL, SQL/PLUS 명령어 온라인 도움말
SQL> HOST //EXIT로 정상 종료하지 않고 호스트 운영체제로 빠져나갔다가 다시 복귀할 수 있다
SQL> TIMING //시스템의 CPU 사용 시간을 보여준다
SQL*PLUS 편집 명령어 (입력되는 모든 정보가 버퍼 영역에서 작업될 때 버퍼 영역을 편집할 수 있다)
SQL> APPEND text
SQL> CHANGE /old/new
SQL> CLEAR BUFFER
SQL> DEL
SQL> DEL x
SQL> DEL y z
SQL> DEL *
SQL> DEL LAST
SQL> GET /경로/파일명
SQL> INPUT
SQL> INPUT text
SQL> LIST no
SQL> LIST y z
SQL> LIST LAST
SQL> SAVE /경로명/파일명
SQL> START
※ SQL*PLUS 사용 시 주의 사항
- CREATE TYPE 또는 CREATE LIBRARY 사용하여 실행할 때는 마지막 라인에 반드시 /를 사용한다.
- 공백 라인을 삽입하지 않는다.
- 주석 라인을 사용할 때 #을 사용하지 않는다.
- 아주 긴 SQL 명령문을 사용하여 다음 라인으로 연속적으로 사용 시 -를 사용하지 않는다.
top
사용자 생성, 변경, 삭제
사용자 생성하기
SQL> CREATE USER [사용자명]
SQL> IDENTIFIED BY [암호]
SQL> DEFAULT TABLESPACE [테이블스페이스명]
SQL> TEMPORARY TABLESPACE [임시 테이블스페이스명]
SQL> QUOTA [숫자]M ON [사용자명]
SQL> PFILE [프로파일명];
사용자 변경하기
SQL> ALTER USER [사용자명]
SQL> IDENTIFIED BY [암호]
SQL> DEFAULT TABLESPACE [테이블스페이스명]
SQL> TEMPORARY TABLESPACE [임시 테이블스페이스명]
SQL> QUOTA [숫자]M ON [사용자명]
SQL> PFILE [프로파일명];
사용자 삭제하기
SQL> DROP USER [사용자명] CASCADE; //사용자가 가지고 있던 테이블, 인덱스 등의 객체를 함께 삭제하는 옵션. 사용 객체가 있는데 CASCADE 옵션을 사용하지 않으면 에러가 날 수 있다
프로파일 생성하기
top
프로파일 생성하기
-프로파일을 사용할 때는 init<DB명>.ora파일에 RESOURCE_LIMIT=TRUE로 설정해야 한다. 패스워드 기능은 FALSE 상태에서도 실행 가능하다.
P.62
패스워드 함수 사용하기
함수를 이용하여 패스워드를 확인하기
SQL> CREATE PROFILE [프로파일명] LIMIT PASSWORD_VERIFY_FUNCTION [함수명];
- {우선 해야할 일} 오라클이 제공하는 검증 함수를 사용하기 위해서는 C:\oracle\ora92\rdbms\admin\utlpwdmg.sql을 실행한다.VERYFY_FUNCTION이라는 함수가 생성된다.
- CREATE OR REPLACE FUNCTION [함수이름] [이하 함수 프로그래밍] 으로 사용자가 함수를 생성할 수도 있다.
- 프로파일을 생성 또는 변경할 때 함수를 설정한다.
패스워드실행과 관련된 옵션절(CREATE USER 혹은 ALTER USER와 함께 사용되는 절)
SQL> PASSWORD EXPIRE
SQL> ACCOUNT UNLOCK
SQL> ACCOUNT LOCK
권한 관리: 시스템 권한
top
시스템 권한 부여하기
SQL> GRANT [시스템권한] TO [사용자명 혹은 PUBLIC]; //PUBLIC은 모든 사용자에게 권한을 부여한다.
SQL> GRANT [시스템권한] TO [사용자명 혹은 PUBLIC] WITH ADMIN OPTION; //부여받은 시스템 권한을 다른 사용자에게 양도할 수 있다.
※ 시스템 권한 종류
CREATE | DROP | ALTER SESSION
CREATE | DROP | ALTER TABLE
CREATE | DROP | ALTER INDEX
CREATE | DROP | ALTER VIEW
CREATE | DROP | ALTER SEQUENCE
CREATE | DROP | ALTER CLUSTER...등등등
시스템 권한 부여 취소하기
SQL> REVOKE [시스템권한,시스템권한..] FROM [사용자명 혹은 PUBLIC];
권한 관리: 객체 권한
top
객체 권한 부여하기
SQL> GRANT [객체권한](컬럼명,컬럼명,..) ON [객체명] TO [사용자명 혹은 PUBLIC] WITH GRANT OPTION;
※ 객체 권한 종류
SELECT
UPDATE
INSERT
ALTER
DELETE
EXECUTE
INDEX //CREATE INDEX ON [테이블명] 문장을 사용할 수 있는 권한
REFERENCES //객체에 대해 외부 키를 정의할 수 있는 권한
객체 권한 부여 취소하기
SQL> REVOKE [객체권한] ON [객체명] FROM [사용자명 혹은 PUBLIC] CASCADE CONSTRAINTS; //CASCADE CONSTRAINTS는 REFERENCES 권한으로 정의된 제약 조건을 함께 삭제하여 준다.
SQL> 


