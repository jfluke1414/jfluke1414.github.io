---
order: 50
title: Oracle wait events
category: Oracledb
---

db file sequential read => tune indexing, tune SQL (to do less I/O), tune disks, increase buffer cache. This event is indicative of disk contention on index reads. Make sure all objects are analyzed. Redistribute I/O across disks. The wait that comes from the physical side of the database. It related to memory starvation and non selective index use. Sequential read is an index read followed by table read because it is doing index lookups which tells exactly which block to go to.
db file scattered read => disk contention on full table scans. Add indexes, tune SQL, tune disks, refresh statistics, and create materialized view. caused due to full table scans may be because of insufficient indexes or unavailability of updated statistics.
• Make money blogging
• Web hosting services
• Twitter marketing strategy
• Oracle Dba
• Twitter for business
db file parallel read => tune SQL, tune indexing, tune disk I/O, increase buffer cache. if you are doing a lot of partition activity then expect to see that wait even. it could be a table or index partition.
db file parallel write => if you are doing a lot of partition activity then expect to see that wait even. it could be a table or index partition.
db file single write => if you see this event than probably you have a lot of data files in your database.

control file sequential read
control file parallel write

log file sync => committing too often, archive log generation is more. Tune applications to commit less, tune disks where redo logs exist, try using nologging/unrecoverable options, log buffer could be too large.
log file switch completion => May need more log files per group.
log file parallel write => Deals with flushing out the redo log buffer to disk. Disks may be too slow or have an I/O bottleneck. Look for log file contention.
log buffer space => Increase LOG_BUFFER parameter or move log files to faster disks. Tune application, use NOLOGGING, and look for poor behavior that updates an entire row when only a few columns change.
log file switch (checkpoint incomplete) => May indicate excessive db files or slow IO subsystem.
log file switch (archiving needed)  => Indicates archive files are written too slowly.
redo buffer allocation retries => shows the number of times a user process waited for space in the redo log buffer. 
redo log space wait time => shows cumulative time (in 10s of milliseconds) waited by all processes waiting for space in the log buffer.

buffer busy waits/ read by other session => Increase DB_CACHE_SIZE. Tune SQL, tune indexing, we often see this event along with full table scans, if the SQL is inserting data, consider increasing FREELISTS and/or INITRANS, if the waits are on segment header blocks, consider increasing extent sizes.
free buffer waits => insufficient buffers, process holding buffers too long or i/o subsystem is over loaded. Also check you db writes may be getting clogged up.
cache buffers lru chain => Freelist issues, hot blocks.
no free buffers => Insufficient buffers, dbwr contention.

latch free
latch: session allocation
latch: in memory undo latch => If excessive could be bug, check for your version, may have to turn off in memory undo.
latch: cache buffer chains => check hot objects.
latch: cache buffer handles => Freelist issues, hot blocks.

direct path write => You wont see them unless you are doing some appends or data loads.
direct path reads => could happen if you are doing a lot of parallel query activity.
direct path read temp or direct path write temp => this wait event shows Temp file activity (sort,hashes,temp tables, bitmap) check pga parameter or sort area or hash area parameters. You might want to increase them.

library cache load lock
library cache pin => if many sessions are waiting, tune shared pool, if few sessions are waiting, lock is session specific.
library cache lock => need to find the session holding the lock, look for DML manipulating an object being accessed, if the session is trying to recompile PL/SQL, look for other sessions executing the code.

undo segment extension => If excessive, tune undo.
wait for a undo record => Usually only during recovery of large transactions, look at turning off parallel undo recovery.

enque wait events => Look at V$ENQUEUE_STAT

SQL*Net message from client
SQL*Net message from dblink
SQL*Net more data from client
SQL*Net message to client
SQL*Net break/reset to client
