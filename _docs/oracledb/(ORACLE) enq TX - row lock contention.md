---
order: 37
title: (ORACLE) enq TX - row lock contention
category: Oracledb
---

enq: TX - row lock contention
Article by Rampant Author Brian Carr
This is indicative of a session waiting for a row lock held by another session; the amount of wait time associated with this wait event is excessive and can be responsible for performance issues observed in the application. TX enqueue are acquired exclusive when a transaction initiates its first change and held until the transaction does a COMMIT or ROLLBACK.
There are several situations of TX enqueue:
Waits for TX in mode 6 occurs when a session is waiting for a row level lock that is already held by another session. This occurs when one user is updating or deleting a row, which another session wishes to update or delete. This type of TX enqueue wait corresponds to the wait event enq: TX - row lock contention.
To solve this you would have the first session already holding the lock perform a COMMIT or ROLLBACK.
Waits for TX in mode 4 can occur if a session is waiting due to potential duplicates in UNIQUE index. If two sessions try to insert the same key value the second session has to wait to see if an ORA-0001 should be raised or not. This type of TX enqueue wait corresponds to the wait event enq: TX - row lock contention.
To solve this again you have the first session already holding the lock perform a COMMIT or ROLLBACK.
Waits for TX in mode 4 is also possible if the session is waiting due to shared bitmap index fragment. Bitmap indexes index key values and a range of ROWIDs. Each ‘entry’ in a bitmap index can cover many rows in the actual table. If two sessions want to update rows covered by the same bitmap index fragment, then the second session waits for the first transaction to either COMMIT or ROLLBACK by waiting for the TX lock in mode 4. This type of TX enqueue wait corresponds to the wait event enq: TX - row lock contention.
Troubleshooting:
For which SQL currently is waiting on:
블록되어있는 쿼리
select sid, sql_text from v$session s, v$sql q where sid in (select sid from v$session where state in ('WAITING') and wait_class != 'Idle' and event='enq: TX - row lock contention' and (q.sql_id = s.sql_id or q.sql_id = s.prev_sql_id));
The blocking session is:
트랜잭션 처리 현황 쿼리
select blocking_session, sid, serial#, wait_class, seconds_in_wait from v$session where blocking_session is not NULL order by blocking_session;
Recommendation: Evaluate the application to look for these situations via the SQL outlined above to determine where the code can be modified to eliminate possible row lock contention items.
