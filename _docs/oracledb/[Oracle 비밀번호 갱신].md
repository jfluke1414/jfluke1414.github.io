---
order: 23
title: Backup.sh
category: Oracledb
---

작업처리 실행 명령어
--정보확인--
SELECT RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE PROFILE='DEFAULT';

--PASSWORD_LIFE_TIME UNLIMITED 변경--
ALTER PROFILE DEFAULT LIMIT PASSWORD_LIFE_TIME UNLIMITED;

--EXPIRY_DATE 확인--
SELECT USERNAME, ACCOUNT_STATUS, LOCK_DATE, EXPIRY_DATE FROM DBA_USERS WHERE USERNAME='TRENDUP20';

--비밀번호 갱신 및 변경--
alter user TRENDUP20 identified by tapaman;



인터넷 예제

oracle 11g 를 설치해서 쓰던 도중...

"비밀번호가 만료되었습니다." 라고 에러가 나서 확인해보니...

따로 설정을 바꾸지 않는 이상 기본으로 180일의 비밀번호 만료 기간이 설정된다고 하는군요!

SQL> SELECT RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE PROFILE='DEFAULT';

RESOURCE_NAME                    LIMIT
-------------------------------- ----------------------------------------
.......

PASSWORD_LIFE_TIME               180

.......

PASSWORD_GRACE_TIME              7
바로 PASSWORD_LIFE_TIME               180 요 부분입니다.

아래와  같이 변경해줍니다.
SQL> ALTER PROFILE DEFAULT LIMIT PASSWORD_LIFE_TIME UNLIMITED;

프로파일이 변경되었습니다.

이미 비밀번호가 만료된 사용자는 다음과 같이 확인할 수 있습니다.
SQL> SELECT USERNAME, ACCOUNT_STATUS, LOCK_DATE, EXPIRY_DATE FROM DBA_USERS WHERE USERNAME='USERNAME';

USERNAME                       ACCOUNT_STATUS                   LOCK_DAT
------------------------------ -------------------------------- --------
EXPIRY_D
--------
USERNAME                       EXPIRED
11/10/04

이 사용자는 아래와 같이 비밀번호를 변경하여 줍니다.
SQL> alter user USERNAME identified by USERNAME;
사용자가 변경되었습니다.

비밀번호 만료가 해제됐는지 확인해봅니다.
SQL> SELECT USERNAME, ACCOUNT_STATUS, LOCK_DATE, EXPIRY_DATE FROM DBA_USERS WHERE USERNAME='USERNAME';

USERNAME                       ACCOUNT_STATUS                   LOCK_DAT
------------------------------ -------------------------------- --------
EXPIRY_D
--------
USERNAME                       OPEN
