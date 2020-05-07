---
title: (ORACLE) Oracle backup(cold backup, hot backup, export backup
category: Oracledb
order: 10
---

오라클 백업에는 크게 피지컬 백업(Physical Backup) 방식과 로지컬 백업(Logical Backup) 방식이 있다. 

피지컬 백업 방식이란 데이타 파일 자체를 카피하는 방식을 말하는데, 이것은 다시 데이타베이스를 셧다운하고 백업하는 방식과 오픈된 상태에서 백업하는 방식으로 나뉜다. 반면, 로지컬 백업 방식이란 오라클에서 제공하는 유틸리티 중의 하나인 Export/Import를 이용하여 백업하는 형식으로, 이 백업 파일을 이용하여 리커버리를 실행하면 Create Object 문장을 이용해 테이블스페이스와 유저, 테이블을 생성하고, Insert Statement를 이용해 특정 테이블에 Insert 작업이 이루어지기 때문에 이처럼 일컫는 것이다. 

먼저 이들에 대해 각각 알아보고, 데이타 복구(Recovery)를 위한 기본 개념들을 다루고자 한다. 그리고 리커버리에 대한 더 구체적인 설명은 다음 호에서 다룰 예정이다. 


Cold Backup 받는 방법 


콜드 백업(Cold Backup)은 데이타베이스가 정상적으로 셧다운된 상태에서 데이타 파일, 로그 파일, 콘트롤 파일을 모두 백업 받는 것을 말한다. 셧다운하지 않고 오픈된 상태에서 백업을 받으면 백업 받은 내용을 나중에 사용할 수가 없으므로 유의해야 한다. 
콜드 백업을 위해서 데이타베이스를 셧다운할 때에는 Normal 또는 Immediate 옵션을 사용해야 하며, Abort를 사용해서는 안 된다. 상황이 여의치 않아 Abort를 사용한 경우에는 셧다운 후에 다시 스타트업하고 Normal로 셧다운한 후 백업을 받도록 한다. 

우선 이들 파일을 백업하기 위해 콘트롤 파일과 데이타 파일 및 로그 파일의 위치를 확인하여 이들을 tar, cpio, dd 등의 명령을 이용하여 백업 받도록 한다. NT에서는 Copy 명령이나 탐색기를 이용해서 백업을 받으면 된다. 

  

■ 콘트롤 파일 확인 방법 
sqlplus에 system/manager로 접속 후 
SQL>select value from v$controlfile; 

■ 데이타 파일 확인 방법 
SQL>select name from v$datafile; 

■ 로그 파일 확인 방법 
SQL>select member from v$logfile; 

  

이처럼 각각의 파일 위치를 확인하여 위에서 확인된 3종류의 파일들을 백업 받으면 된다. 이때 오라클은 반드시 셧다운된 상태이어야 한다. 항상은 아니지만 필요에 따라서는 패러미터 파일까지 받아두는 것이 좋다. 패러미터 파일은 $ORACLE_HOME/dbs/init.ora에 있는데, 이 초기화 패러미터 파일에 기술되어진 패러미터는 시스템의 성능에 주요한 역할을 하므로 이 파일이 없어진 경우에 예전의 성능을 유지하려면 이 파일을 필수적으로 백업해야 한다. 

  

NT에서는 C:\ORANT\DATABASE\init.ora 파일이다. 

일반적으로 NT의 SID가 처음 만들어질 때 ORCL이므로 이 초기 패러미터 파일 역시 initORCL.ora라고 되어 있다. 

여기서 는 오라클 인스턴스 이름으로 환경변수 ORACLE_SID로 지정되어 있다. 이 ORACLE_SID는 Unix의 경우 $env, NT의 경우는 Registry에 지정되어 있으므로 직접 확인해 볼 수 있다. 


Hot Backup 받는 방법 


핫 백업(Hot Backup)이란 데이타베이스를 셧다운하지 않고 백업하는 방식으로, 일반적인 경우는 적용되지 않고 자신의 데이타베이스를 Archive Mode로 운영하는 경우에만 가능하다. 콜드 백업을 이용하여 데이타를 복구하는 경우에는 콜드 백업을 받은 시점까지만 복구가 가능한 데 반해, 이 Archive 방식으로 데이타베이스를 운영하는 경우에는 사용자가 원하는 시점까지 데이타를 복구할 수 있다. 즉, 원하는 시간을 주어서, SCN 번호를 주어서, 혹은 어느 데이타 파일 한 개만의 복구도 가능하다. 

데이타 복구만 생각한다면 모든 데이타베이스를 Archive 방식으로 운영하는 것이 좋겠지만, 이 방식을 사용하는 경우 데이타베이스 관리자가 백업/리커버리에 관하여 많은 지식과 경험을 갖춰야 하며, 또 Archive Log를 계속 유지관리하는 데는 스페이스와 성능의 부하가 따르기 때문에 사용자의 적절한 판단에 의하여 이용하도록 한다. 

그러면 Archive Log Mode의 운영 방법에 대해 알아보자. 


Archive Log Mode 운영 방법 


오라클에서 데이타베이스가 셧다운되지 않은 상태에서 백업을 받거나 문제가 생긴 시점까지의 완벽한 리커버리 작업을 수행하기 위해서는 데이타베이스를 아카이브 로그 모드로 운영하여야 한다. 

아카이브 로그 모드로 운영하기 위해서는 다음의 절차에 따라 변경하여야 한다. 

  

1. initSID.ora 파일과 configSID.ora에 다음의 패러미터가 이미 설정되어 있는지 확인한 후에 없을 경우 initSID.ora에 설정한다. 

(1) LOG_ARCHIVE_START = TRUE 

이 패러미터에 의해 데이타베이스가 처음 구동시 ARCH 프로세스가 기동. 

Log Switch 발생시 Automatic Archive를 수행한다. 

만약 이 패러미터가 False이면 Manual Archive를 수행한다. 
(2)LOG_ARCHIVE_DEST =/home/oracle8/dbs/archive_file/arc 
아카이브 파일이 생성되는 위치인 디렉토리와 확장자를 포함하지 않는 파일명을 지정. 

여기에서 archive_file까지는 디렉토리이며 마지막에 있는 arc는 아카이브 로그 파일 이름의 첫 부분이다. 
이 아카이브 로그 모드를 설정하면 로그 파일의 스위치가 일어날 때마다 지속적으로 이 Log_Archive_Dest에 지정한 위치에 로그 파일이 쌓이게 되는데, 만일 부주의에 의해 이 아카이브 로그 파일이 깨지거나 분실되는 경우는 그 이후의 데이타 복구가 불가능하므로 주의하여야 한다. 

이러한 문제를 줄이기 위해 Oracle8부터는 아카이브 로그 파일을 Mirroring하기 위하여 여러 군데에 보관할 수 있는 방안도 도입되었다. 이는 log_archive_duplex_dest를 설정함으로써 가능하다. 

또한 V8i부터는 최대 5군데에 이 로그 파일을 저장할 수 있도록 하여 

LOG_ARCHIVE_DEST_1=”LOCATION=/oracle8/arch_1 MANDATORY” 
LOG_ARCHIVE_DEST_2=”LOCATION=/oracle8/arch_2 OPTIONAL? 

처럼 지정이 가능하다 

(3) LOG_ARCHIVE_FORMAT = %s.log 
아카이브 파일의 확장자와 로그 시퀀스 번호의 형식을 지정. 

이는 (2)에서 정의된 아카이브 로그 파일의 첫 부분 이름과 함께 나타난다. 
arc123.log, arc124.log (123과 124는 로그 시퀀스 번호) 와 같은 형태의 파일이 지정한 위치에 생성된다. 

  

2. 다음과 같이 작업하여 아카이브 로그 모드로 변환한다. 

$ svrmgrl 

SVRMGR> connect internal 
SVRMGR> startup mount - ■ 
SVRMGR> alter database archivelog; - □ 
SVRMGR> archive log list - ● 
Database log mode ARCHIVELOG - ◎ 
Automatic archival ENABLED - ◇ 
Archive destination ?/dbs_ar/offline_log/offline - ◆ 
Oldest online log sequence 123 - △ 
Next log sequence to archive 125 - ▲ 
Current log sequence 125 - ▷ 
SVRMGR> alter database open; - ▶ 

■ DB를 Startup Mount까지만 한다. 
□ 이 커맨드를 이용하여 아카이브 모드로 데이타베이스를 변경한다. 
● 아카이브 모드로 변경되었는지를 확인한다. 
◎ 데이타베이스가 아카이브 모드임을 나타낸다. 만약 NOARCHIVELOG로 되어 있으면 변경되지 않은 것을 의미한다. 
◇ initSID.ora 파일에서 LOG_ARCHIVE_START 패러미터를 TRUE로 정의하였음을 나타내며 False인 경우에는 DISABLED로 나타난다. 
◆ initSID.ora 파일의 LOG_ARCHIVE_DEST 패러미터에서 정의한 아카이브할 장소이다. 
△ 3개의 Redo Log 중 가장 오래된 리두 로그의 시퀀스가 123임을 의미한다. 
▲ 다음에 아카이브 받을 파일의 로그 시퀀스 번호를 나타낸다. 
▷ 현재 사용중인 리두 로그의 시퀀스가 125임을 의미한다. 만약 이전부터 아카이브 로그 모드로 운영중이었다면 여기에서 아카이브 로그 파일은 로그 시퀀스 124까지 아카이브되어 있다는 것을 의미한다. 
▶ 아카이브 모드로 변경 후 DB를 오픈한다. 


No Archive Log Mode로 전환하는 방법 
반대로, Archivelog Mode에서 No Archivelog Mode로 전환하는 방법은 다음과 같다. 

먼저, 위에서 세팅했던 initSID.ora 파일과 configSID.ora에 있는 다음 패러미터 앞에 #을 넣고 저장한다. 
#LOG_ARCHIVE_START = TRUE 
#LOG_ARCHIVE_DEST = /home/oracle8/dbs/archive_file/arc 
#LOG_ARCHIVE_FORMAT = %s.log 

$ svrmgrl 
SVRMGR> connect internal; 
SVRMGR> shutdown immediate 
SVRMGR> startup mount 
ORACLE instance started. 
Database mounted. 
SVRMGR> alter database noarchivelog; 
Statement processed. 
SVRMGR> alter database open; 
Statement processed. 


Hot Backup 하는 방법 


데이타베이스를 셧다운하지 않고 데이타 파일을 백업하는 방법이다. 
이 방법은 콜드 백업보다 더 복잡하지만 데이타베이스가 오픈되어 있는 도중에 할 수 있고 또한 테이블스페이스 별로 백업할 수 있다는 장점이 있다. 
핫 백업은 항상 데이타베이스를 아카이브 로그 모드 상태로 두고 실시한다. 

| 방법 | 테이블스페이스 단위로 백업을 실시한다. 
svrmgrl > CONNECT INTERNAL 

svrmgrl > ALTER TABLESPACE SYSTEM BEGIN BACKUP; 

시스템 테이블스페이스의 모든 데이타파일에 대해서 OS Backup 한다. 

$ tar cvf /dev/rmt0 /usr/oracle8/dbs/syst1ORA8.dbf 

$ tar cvf /dev/rmt0 /usr/oracle8/dbs/syst2ORA8.dbf 

svrmgrl > ALTER TABLESPACE SYSTEM END BACKUP; 

svrmgrl > ALTER TABLESPACE USERS BEGIN BACKUP; 

$ tar cvf /dev/rmt0 /usr/oracle8/dbs/user1ORA8.dbf 

svrmgrl > ALTER TABLESPACE USERS END BACKUP; 

다른 테이블스페이스에 대해서도 같은 방법으로 한다. 


주의할 점은 BEGIN과 END 사이에는 해당 테이블스페이스의 데이타파일 헤더 정보가 변경되지 않는다는 것이다. 따라서 OS 백업이 종료됨과 동시에 ‘ALTER TABLESPACE ... END BAKCUP’ 커맨드를 실행하여 데이타파일의 헤더가 변경되도록 한다. 
이 아카이브 백업 파일을 이용한 복구 방법은 다음 기회에 다루도록 한다. 


Export Backup 하는 방법 


오라클에서 제공되는 Export 유틸리티는 데이타베이스에 저장된 데이타를 바이너리 형태의 OS 파일로 만들고, 필요시 Import 유틸리티를 이용하여 데이타베이스로 다시 올리는 방식이다 . 
이 유틸리티는 각 오브젝트 단위로 처리가 가능하기 때문에 테이블 몇 개만을 복구한다든가 특정 사용자의 테이블들을 다른 테이블스페이스로 옮긴다든가 또는 전체 데이타베이스의 자료를 서로 다른 OS로 옮기는 경우 등에 특히 유리하다. 


Export의 종류 


이 Export 방안은 시스템과 서로 메시지를 주고받으면서 백업을 할 수 있는 Interactive Mode가 있고, 한 라인의 명령어로 Export시 필요한 옵션을 길게 열거해주는 Command 방식이 있다. 
Command 방식은 순간 순간 필요한 옵션을 적어주기만 하면 되기 때문에 여기서는 Interactive 방식을 다루어 보기로 한다 


Export의 단위 

  

Full 단위 : 전체 데이타베이스를 Export 한다. 
User 단위 : 특정 유저 전체 오브젝트를 Export 한다. 
Table 단위 : 특정 테이블을 Export 한다. 
Partition 단위 : 특정 테이블의 파티션을 Export 한다. 

Export의 실제 예제 
| 예 1 | 전체 데이타베이스의 Export (Interactive Method) 

$ exp system/manager 
Connected to: ORACLE8 Server Release 8.0.5 - Production 

With the procedural and distributed options 
PL/SQL Release 2.2 - Production 
Enter array fetch buffer size : 4096 > 100000 (RETURN) 
Export file : expdat.dmp > 
(1) E(ntire database), (2) U(sers), (3) T(ables) : U > e 
Export grants (Y/N) : Y > y 
Export table data (Y/N) : Y > y 
Compress extents (Y/N) : Y > y 
About to export the entire database.... 

. exporting tablespace definitions 
. exporting profiles 
. exporting user definitions 
. exporting role 
. exporting rollback segment definitions 
. exporting database links 
. exporting sequence numbers 
. exporting sequence numbers 
. exporting cluster definitions 
. exporting stored procedures 
. about to export SYSTEM’s tables ... 
. about to export SCOTT’s tables ... 
. exporting synonyms 
. exporting views 
. exporting referential integrity constraints 
. exporting triggers 

Export terminated successfully without warnings. 
| 예 2 | 전체 데이타베이스의 EXPORT(Command Line Method) 

$ exp userid=system/manager full=y file=fullbackup.dmp buffer=100000 
| 예 3 | 전체 데이타베이스의 EXPORT(Dynamic Method) 
Export 패러미터를 다음과 같은 파일(tusc.par) 형태로 만든다. 

system/manager 
full=y 
file=fullbackup.dmp 
buffer=100000 
$ exp parfile=tusc.par 

| 예 4 | User 단위의 Export 

$ exp system/manager 
Connected to: ORACLE8 Server Release 8.0.5 - Production 

With the procedural and distributed options 
PL/SQL Release 2.2 - Production 
Enter array fetch buffer size : 4096 > 100000 (RETURN) 
Export file : expdat.dmp > 
(1) E(ntire database), (2) U(sers), (3) T(ables) : U > u 
Export grants (Y/N) : Y > y 
Export table data (Y/N) : Y > y 
Compress extents (Y/N) : Y > y 

About to export specified users 
User to be exported: (RETURN to quit) > scott 
. exporting snapshots 
. exporting snapshot log 
. exporting database links 
. exporting sequence numbers 
. exporting sequence numbers 
. exporting cluster definitions 
. exporting stored procedures 
. about to export SCOTT’s tables ... 
. exporting synonyms 
. exporting views 
. exporting referential integrity constraints 
. exporting triggers 
Export terminated successfully without warnings. 

| 예 5 | User 단위의 Export (Command Line Method) 

$ exp system/manager owner=scott file=scott.dmp buffer=100000 

또는 

$ exp scott/tiger file=scott.dmp buffer=100000 

| 예 6 | User 단위의 Export (Dynamic Method ) 
Export 패러미터를 다음과 같은 파일(tusc.par) 형태로 만든다. 

$vi tusc.par 

scott/tiger 
file=scott.dmp 
buffer=1000000 
$ exp parfile=tusc.par 

| 예 7 | Table 단위의 Export 

$ exp scott/tiger file=table.dmp tables=emp,dept buffer=100000  
