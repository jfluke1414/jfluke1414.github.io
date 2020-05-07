---
title: (ORACLE) Oracle 사용자 패스워드 사용기간 제한 없애기
category: Oracledb
order: 19
---

0. SYSTEM 계정으로 접속

1. -- DBA 유저들 확인 --
select username, account_status, expiry_date, profile from dba_users;

-- Expire Date 확인 --
2. select * from dba_profiles where profile = 'DEFAULT'

3. -- Unlimited 변경 --
alter profile default limit password_life_time unlimited;

4. -- 비밀번호 재변경
ALTER USER [User ID] IDENTIFIED BY [Password];
ALTER USER system IDENTIFIED BY tapaman;

5. -- 변경 확인 --
SELECT USERNAME, ACCOUNT_STATUS, LOCK_DATE, EXPIRY_DATE
FROM DBA_USERS
WHERE USERNAME = 'TRENDUP20'
ORDER BY CREATED;
