---
title: (ORACLE) Backup.sh
category: Oracledb
order: 22
---

more backup.sh
export ORACLE_BASE=/oracle/app/oracle
export ORACLE_HOME=/oracle/app/oracle/product/11.2.0/dbhome_1
export ORACLE_SID=orcl
#backup trendup20
rm -f /home/backup/*bak
mv -f /home/backup/trendup20.dmp /home/backup/trendup20.dmp.bak
/oracle/app/oracle/product/11.2.0/dbhome_1/bin/exp trendup20/tapaman file=/home/backup/trendup20.dmp log=/home/backup/trendup20.log 
buffer=10240000

#backup trendsrch20.dmp
#rm -f /oracle/backup/*bak
#mv -f /oracle/backup/trendsrch20.dmp /oracle/backup/trendsrch20.dmp.bak
rm -f /oracle/backup/trendsrch20.dmp
/oracle/app/oracle/product/11.2.0/dbhome_1/bin/exp trendsrch20/tapaman file=/oracle/backup/trendsrch20.dmp log=/oracle/backup/trends
rch20.log buffer=10240000



