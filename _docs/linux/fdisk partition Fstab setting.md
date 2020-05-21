---   
order: 50   
title: (LINUX) fdisk partition Fstab setting   
category: Linux   
---   
   
#파티션 생성부터 포맷 마운트   
    
 ■ 간단한 예제와 함께 적어보도록 하겠습니다.   
    
■ EX) 100m 의 새 파티션을 생성하고 /data 로 마운트를 시켜라   
          단 파일시스템은 ext3 로 설정.   
    
### 1. 파티션생성   
    
 [root@mail root]#fdisk /dev/hda     
  The number of cylinders for this disk is set to 9733.   
  There is nothing wrong with that, but this is larger than 1024,   
  and could in certain setups cause problems with:     
  1) software that runs at boot time (e.g., old versions of LILO)   
  2) booting and partitioning software from other OSs   
  (e.g., DOS FDISK, OS/2 FDISK)   
Command (m for help): n    
  First cylinder (9004-9733, default 9004):     
  Using default value 9004   
  Last cylinder or +size or +sizeM or +sizeK (9004-9733, default 9733): +100m    
     
  Command (m for help): p   
    
  Disk /dev/hda: 80.0 GB, 80060424192 bytes   
 255 heads, 63 sectors/track, 9733 cylinders   
 Units = cylinders of 16065 * 512 = 8225280 bytes   
   
 Device        Boot   Start   End         Blocks        Id    System    
 /dev/hda1     * 1            3824         30716248+     7    HPFS/NTFS   
 /dev/hda2            3825   5099         10241437+   83     Linux   
 /dev/hda3            5100   5230         1052257+    82     Linux swap   
 /dev/hda4            5231   9733         36170347+    5     Extended   
 /dev/hda5            5231   7055         14659281     fd     Linux raid autodetect   
 /dev/hda6            7056   8880         14659281     fd     Linux raid autodetect   
 /dev/hda7            8881   9003         987966       83     Linux   
 /dev/hda8            9004   9016         104391       83     Linux   
    
※ 세부설명은 현 블로그에 LINUX FDISK 참조   
    
### 2. 포맷 (= 파일시스템 지정)   
    
[root@mail root]#mkfs -t ext3 /dev/hda8   
                                 └파일시스템지정    
    
### 3. /data 마운트 시키기   
    
[root@mail root]# mkdir /data   
  -> 마운트 시킬 /data 디렉토리를 생성한다.   
    
[root@mail root]# mount -t ext3 /dev/hda7 /data   
  -> /dev/hda8 을 /data 디렉토리로 마운트 시킨다.   
    
[root@mail root]# mount   
/dev/hda2 on / type ext3 (rw)   
none on /proc type proc (rw)   
usbdevfs on /proc/bus/usb type usbdevfs (rw)   
none on /dev/pts type devpts (rw,gid=5,mode=620)   
none on /dev/shm type tmpfs (rw)   
automount(pid4742) on /home type autofs (rw,fd=5,pgrp=4742,minproto=2,maxproto=3)   
/dev/hda8 on /data type ext3 (rw)   
  └ 마운트된것을 확인할수 있다.   
    
### 4.fstab 등록하기   
    
-> 재부팅할경우 마운트명령으로 마운트 시킨건 다시 마운트 되지 않는다.   
    그러므로 /etc/fstab 에 등록시켜야한다.   
[root@mail root]# cat /etc/fstab   
LABEL=/ / ext3 defaults 1 1   
none /dev/pts devpts gid=5,mode=620 0 0   
none /proc proc defaults 0 0   
none /dev/shm tmpfs defaults 0 0   
/dev/hda3 swap swap defaults 0 0   
/dev/cdrom /mnt/cdrom udf,iso9660 noauto,owner,kudzu,ro 0 0   
/dev/fd0 /mnt/floppy auto noauto,owner,kudzu 0 0   
#/dev/md0 /var ext3 defaults 0 0   
#//203.247.50.229/project /wjdgns smbfs defaults,noauto 0 0   
 -> 원래 fstab 정보   
   
[root@mail root]# cat /etc/fstab   
LABEL=/ / ext3 defaults 1 1   
none /dev/pts devpts gid=5,mode=620 0 0   
none /proc proc defaults 0 0   
none /dev/shm tmpfs defaults 0 0   
/dev/hda3 swap swap defaults 0 0   
/dev/cdrom /mnt/cdrom udf,iso9660 noauto,owner,kudzu,ro 0 0   
/dev/fd0 /mnt/floppy auto noauto,owner,kudzu 0 0   
#/dev/md0 /var ext3 defaults 0 0   
#//203.247.50.229/project /wjdgns smbfs defaults,noauto 0 0   
/dev/hda7 /data ext3 defaults 0 0   
└ 위와같이 등록시키면 부팅시마다 마운트된다.   
   
   
■ /etc/fstab 이나 fdisk 안의 내용은 제 컴의 예제이므로 다를수있습니다.