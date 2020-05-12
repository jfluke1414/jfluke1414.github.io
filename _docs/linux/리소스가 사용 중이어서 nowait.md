---
order: 66
title: (LINUX) 리소스가 사용 중이어서 nowait
category: Linux
---

# session kill
SELECT a.session_id AS SESSION_ID, b.serial# AS SERIAL_NO,
a.os_user_name AS OS_USER_NAME, a.oracle_username AS ORACLE_USERNAME, b.status AS STATUS
FROM v$locked_object a, v$session b
WHERE a.session_id = b.sid;

상단의 쿼리를 실행하여 나온 SESSION_ID와 SERIAL_NO를 하단의 쿼리에 값으로 넣어서 실행한다.

alter system kill session 'SESSION_ID,SERIAL_NO';

다수의 사용자가 하나의 DB로 작업하다가 lock이 걸리는 경우는
선행 사용자가 commit 해주면 간단히 해결되는 경우가 있다.


또한, commit으로 해결되지 않으면
상단에 작성한 session kill 방법을 이용해도 해결이 가능하다.
