---
order: 63
title: (LINUX) Setting ISCSI
category: Linux
---

Parted /dev/*** 이용한 파티션 작업
mkpart sda1 0 2000000
mkpart sda2 2000000 4000000
mkpart sda3 4000000 6000000
mkpart sda4 6000000 8000000
mkpart sda5 8000000 8500000
mkpart sda6 8500000 8600000
mkpart sda7 8600000 100%


-- target 생성
tgtadm --lld iscsi --op new --mode target --tid 1 -T aaron_Backup
tgtadm --lld iscsi --op new --mode target --tid 2 -T aaron_Backup
tgtadm --lld iscsi --op new --mode target --tid 3 -T aaron_DB
tgtadm --lld iscsi --op new --mode target --tid 4 -T aaron
tgtadm --lld iscsi --op new --mode target --tid 5 -T aaron_Backup
tgtadm --lld iscsi --op new --mode target --tid 6 -T aaron_Backup

-- target volume bind 할당
tgtadm --lld iscsi --op new --mode logicalunit --tid 1 --lun 1 -b /dev/sda1
tgtadm --lld iscsi --op new --mode logicalunit --tid 2 --lun 2 -b /dev/sda2
tgtadm --lld iscsi --op new --mode logicalunit --tid 3 --lun 3 -b /dev/sda3
tgtadm --lld iscsi --op new --mode logicalunit --tid 4 --lun 4 -b /dev/sda4
tgtadm --lld iscsi --op new --mode logicalunit --tid 5 --lun 5 -b /dev/sda5
tgtadm --lld iscsi --op new --mode logicalunit --tid 6 --lun 6 -b /dev/sda6

-- target 확인
tgtadm --lld iscsi --op show --mode target


-- target 삭제
tgtadm --lld iscsi --op delete --mode target --tid 1
tgtadm --lld iscsi --op delete --mode target --tid 2
tgtadm --lld iscsi --op delete --mode target --tid 3
tgtadm --lld iscsi --op delete --mode target --tid 4
tgtadm --lld iscsi --op delete --mode target --tid 5
tgtadm --lld iscsi --op delete --mode target --tid 6


-- target initiator 접근 제한
tgtadm --lld iscsi --op bind --mode target --tid 1 -I ALL
tgtadm --lld iscsi --op bind --mode target --tid 2 -I ALL
tgtadm --lld iscsi --op bind --mode target --tid 3 -I ALL
tgtadm --lld iscsi --op bind --mode target --tid 4 -I ALL
tgtadm --lld iscsi --op bind --mode target --tid 5 -I ALL
tgtadm --lld iscsi --op bind --mode target --tid 6 -I ALL


tgtadm --lld iscsi --op bind --mode target --tid 1 -I 10.10.10.74
tgtadm --lld iscsi --op bind --mode target --tid 2 -I 10.10.10.122
tgtadm --lld iscsi --op bind --mode target --tid 5 -I 10.10.10.69
tgtadm --lld iscsi --op bind --mode target --tid 6 -I 10.10.10.148

initiator에서의 작업
-- initator 설치
yum install iscsi-initiator-utils

-- 환경설정
vi /etc/iscsi/iscsid.conf 설정 수정


-- target 찾기
iscsiadm --mode discovery --type sendtargets --portal 10.10.10.173

-- target 로그인
iscsiadm --mode node --targetname aaron_Backup --portal 10.10.10.173 --login
iscsiadm --mode node --targetname aaron_Backup --portal 10.10.10.173 --login
iscsiadm --mode node --targetname aaron_DB --portal 10.10.10.173 --login
iscsiadm --mode node --targetname aaron --portal 10.10.10.173 --login
iscsiadm --mode node --targetname aaron_Backup --portal 10.10.10.173 --login
iscsiadm --mode node --targetname aaron_Backup --portal 10.10.10.173 --login


-- target 로그아웃
iscsiadm --mode node --targetname aaron_Backup --portal 10.10.10.173 --logout
iscsiadm --mode node --targetname aaron_Backup --portal 10.10.10.173 --logout
iscsiadm --mode node --targetname aaron_Backup --portal 10.10.10.173 --logout
iscsiadm --mode node --targetname aaron_Backup --portal 10.10.10.173 --logout
iscsiadm --mode node --targetname aaron_DB --portal 10.10.10.173 --logout
iscsiadm --mode node --targetname aaron --portal 10.10.10.173 --logout

iscsiadm --mode node --targetname aaron_Backup --portal 192.168.5.123 --logout
iscsiadm --mode node --targetname aaron_Backup --portal 192.168.5.123 --logout
iscsiadm --mode node --targetname aaron_Backup --portal 192.168.5.123 --logout
iscsiadm --mode node --targetname aaron_Backup --portal 192.168.5.123 --logout
iscsiadm --mode node --targetname aaron_DB --portal 192.168.5.123 --logout
iscsiadm --mode node --targetname aaron --portal 192.168.5.123 --logout

-- fstab 설정
/dev/sda1               /aaron_Backup    ext4    _netdev         0 0
/dev/sdb1               /aaron_DB         ext4    _netdev         0 0
/dev/sde1               /aaron_Backup      ext4    _netdev         0 0
/dev/sdd1               /aaron_Backup       ext4    _netdev         0 0
/dev/sdb1               /aaron_Backup         ext4    _netdev         0 0
