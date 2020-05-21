---   
order: 44   
title: (LINUX) linux add dev   
category: Linux   
---   
   
### 1. 새로운 하드 디스크 추가   
새로운 하드 디스크를 추가한 후 시스템을 재부팅한다.   
재부팅이 완료되면 제대로 인식이 되는지 확인한다.   
IDE 하드 디스크의 경우 /dev/hd[a-z], SCSI 하드 디스크의 경우 /dev/sd[a-z] 로 표기된다.   
   
# dmesg | grep hdb    
    ide0: BM-DMA at 0xf000-0xf007, BIOS settings: hda:pio, hdb:pio   
hdb: ST380011A, ATA DISK drive   
hdb: max request size: 512KiB   
hdb: Host Protected Area detected.   
hdb: Host Protected Area disabled.   
hdb: 156301488 sectors (80026 MB) w/2048KiB Cache, CHS=16383/255/63, UDMA(33)   
hdb: cache flushes supported   
 hdb:   
hdb: drive_cmd: status=0x51 { DriveReady SeekComplete Error }   
hdb: drive_cmd: error=0x04 { DriveStatusError }   
#   
# ls /dev/hd*   
/dev/hda   /dev/hda2  /dev/hda4  /dev/hda6  /dev/hdb   
/dev/hda1  /dev/hda3  /dev/hda5  /dev/hda7  /dev/hdc   
    
### 2. fdisk 를 통한 파티션 생성   
   
# fdisk -l          // 현재의 디스크 상태 확인   
Disk /dev/hda: 80.0 GB, 80026361856 bytes   
255 heads, 63 sectors/track, 9729 cylinders   
Units = cylinders of 16065 * 512 = 8225280 bytes   
   Device Boot      Start         End      Blocks   Id  System   
/dev/hda1   *           1          13      104391   83  Linux   
/dev/hda2              14        2563    20482875   83  Linux   
/dev/hda3            2564        5113    20482875   83  Linux   
/dev/hda4            5114        9729    37078020    5  Extended   
/dev/hda5            5114        6388    10241406   83  Linux   
/dev/hda6            6389        6649     2096451   82  Linux swap / Solaris   
/dev/hda7            6650        9729    24740068+  83  Linux   
Disk /dev/hdb: 80.0 GB, 80026361856 bytes       // hdb 디스크는 인식되지만 파티션은 없음.   
255 heads, 63 sectors/track, 9729 cylinders   
Units = cylinders of 16065 * 512 = 8225280 bytes   
   Device Boot      Start         End      Blocks   Id  System   
#   
# fdisk /dev/hdb    // hdb 디스크 파티션 설정을 위해 fdisk 실행   
The number of cylinders for this disk is set to 9729.   
There is nothing wrong with that, but this is larger than 1024,   
and could in certain setups cause problems with:   
1) software that runs at boot time (e.g., old versions of LILO)   
2) booting and partitioning software from other OSs   
   (e.g., DOS FDISK, OS/2 FDISK)   
Command (m for help): m   
   a   toggle a bootable flag   
   b   edit bsd disklabel   
   c   toggle the dos compatibility flag   
   d   delete a partition                    // 파티션 삭제   
   l   list known partition types          // 파티션 타입 리스트   
   m   print this menu   
   n   add a new partition                 // 새 파티션 생성   
   o   create a new empty DOS partition table   
   p   print the partition table             // 파티션 테이블 보여주기   
   q   quit without saving changes     // fdisk 종료   
   s   create a new empty Sun disklabel   
   t   change a partition's system id   // 파티션의 시스템 id 변경   
   u   change display/entry units   
   v   verify the partition table   
   w   write table to disk and exit      // 저장 후 종료   
   x   extra functionality (experts only)   
Command (m for help):   
Command (m for help): p    // 현재의 상태 확인   
Disk /dev/hdb: 80.0 GB, 80026361856 bytes   
255 heads, 63 sectors/track, 9729 cylinders   
Units = cylinders of 16065 * 512 = 8225280 bytes   
   Device Boot      Start         End      Blocks   Id  System   // 아무것도 없음   
Command (m for help):   
Command (m for help): n    // 새로운 파티션 생성   
Command action   
   e   extended                  // 기존 하드 디스크가 1-4까지 모두 사용했다면 확장 파티션 사용   
   p   primary partition (1-4) // 기존 하드 디스크의 파티션이 남아 있다면 primary 파티션 사용   
e       // 상단의 fdisk에서 확인한 결과 hda4가 extend로 나와 있으므로 이미 확장 파티션을 사용중이다.   
         // 새로운 하드 디스크도 확장 디스크로 연결해야 한다.   
Partition number (1-4): 1   
First cylinder (1-9729, default 1):  // 파티션의 시작점을 입력. 처음이므로 그냥 엔터를 친다.   
Using default value 1   
Last cylinder or +size or +sizeM or +sizeK (1-9729, default 9729):  // 파티션의 끝을 입력. 파티션을 하나로 할 경우 그냥 엔터   
Using default value 9729                                                           // 파티션을 용량별로 나누려면 +500M 식으로 입력.   
Command (m for help):   
Command (m for help): p   
Disk /dev/hdb: 80.0 GB, 80026361856 bytes   
255 heads, 63 sectors/track, 9729 cylinders   
Units = cylinders of 16065 * 512 = 8225280 bytes   
   Device Boot      Start         End      Blocks   Id  System   
/dev/hdb1               1        9729    78148161    5  Extended   
Command (m for help): n   // 확장 파티션 아래 논리 파티션을 생성한다.   
Command action   
   l   logical (5 or over)   
   p   primary partition (1-4)   
l   
First cylinder (1-9729, default 1):   
Using default value 1   
Last cylinder or +size or +sizeM or +sizeK (1-9729, default 9729):   
Using default value 9729   
Command (m for help): p   
Disk /dev/hdb: 80.0 GB, 80026361856 bytes   
255 heads, 63 sectors/track, 9729 cylinders   
Units = cylinders of 16065 * 512 = 8225280 bytes   
   Device Boot      Start         End      Blocks   Id  System   
/dev/hdb1               1        9729    78148161    5  Extended  // 확장 파티션   
/dev/hdb5               1        9729    78148129+  83  Linux       // 논리 파티션. 실제로 이 파티션이 마운트 된다.   
Command (m for help): w    // 파티션 설정을 마쳤으면 저장을 하고 빠져나온다.   
The partition table has been altered!   
Calling ioctl() to re-read partition table.   
Syncing disks.   
#   
# fdisk -l   // 파티션 정보를 다시 확인   
Disk /dev/hda: 80.0 GB, 80026361856 bytes   
255 heads, 63 sectors/track, 9729 cylinders   
Units = cylinders of 16065 * 512 = 8225280 bytes   
   Device Boot      Start         End      Blocks   Id  System   
/dev/hda1   *           1          13      104391   83  Linux   
/dev/hda2              14        2563    20482875   83  Linux   
/dev/hda3            2564        5113    20482875   83  Linux   
/dev/hda4            5114        9729    37078020    5  Extended   
/dev/hda5            5114        6388    10241406   83  Linux   
/dev/hda6            6389        6649     2096451   82  Linux swap / Solaris   
/dev/hda7            6650        9729    24740068+  83  Linux   
Disk /dev/hdb: 80.0 GB, 80026361856 bytes   
255 heads, 63 sectors/track, 9729 cylinders   
Units = cylinders of 16065 * 512 = 8225280 bytes   
   Device Boot      Start         End      Blocks   Id  System   
/dev/hdb1               1        9729    78148161    5  Extended   // 새로운 하드 디스크의 파티션이 확인 된다.   
/dev/hdb5               1        9729    78148129+  83  Linux   
#   
    
### 3. ext3 파일 시스템으로 파티션 포맷   
파일 시스템의 종류는 ext2, ext3 방식이 있다.   
이 중 복구 능력이 있는 ext3 방식을 통해 포맷을 진행하도록 한다.   
   
mkfs -t ext4 /dev/sdd1   
# mke2fs -j /dev/hdb5    // etc3 파일 시스템으로 /dev/hdb5 포맷   
mke2fs 1.39 (29-May-2006)   
Filesystem label=   
OS type: Linux   
Block size=4096 (log=2)   
Fragment size=4096 (log=2)   
9781248 inodes, 19537032 blocks   
976851 blocks (5.00%) reserved for the super user   
First data block=0   
Maximum filesystem blocks=0   
597 block groups   
32768 blocks per group, 32768 fragments per group   
16384 inodes per group   
Superblock backups stored on blocks:	   
        32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,   
        4096000, 7962624, 11239424   
Writing inode tables: done   
Creating journal (32768 blocks): done   
Writing superblocks and filesystem accounting information: done   
This filesystem will be automatically checked every 22 mounts or   
180 days, whichever comes first.  Use tune2fs -c or -i to override.   
#   
    
### 4. 마운트   
새로운 하드 디스크를 사용하기 위해서는 디렉토리 생성 후 해당 디렉토리로 마운트를 해줘야 한다.   
마운트는 시스템이 재부팅하면 해제되므로 /etc/fstab 파일에 정보를 입력하여 계속해서 마운트 할 수 있도록 한다.   
   
# mount -t ext3 /dev/hdb5 /data   // /dev/hdb5 를 /data 로 ext3 형식으로 마운트   
# cd /data             // data 폴더로 진입 후 폴더 내부를 ls 해 보면 lost+found 라는 디렉토리가 있음을 확인할 수 있다.   
# ls                      // lost+found 라는 디렉토리는 하나의 파티션에 하나만 생성되는 디렉토리이다.   
lost+found             // 즉 정상적으로 마운트가 됐음을 의미한다.   
# vi /etc/fstab    // 시스템 재부팅 후에도 적용될 수 있도록 /etc/fstab 파일 수정   
   
LABEL=/1                      /                        ext3    defaults                1 1   
LABEL=/home                /home                 ext3    defaults                1 2   
LABEL=/usr1                  /usr                   ext3    defaults                 1 2   
LABEL=/var1                  /var                    ext3    defaults                1 2   
LABEL=/boot                  /boot                  ext3    defaults                1 2   
tmpfs                             /dev/shm            tmpfs   defaults                0 0   
devpts                           /dev/pts             devpts  gid=5,mode=620     0 0   
sysfs                             /sys                   sysfs   defaults                0 0   
proc                              /proc                  proc    defaults                0 0   
LABEL=SWAP-hda6         swap                 swap    defaults               0 0   
/dev/hdb5               /data              ext3    defaults          1 2  // 이 부분 추가   
wq!   
#   
    
### 5. 확인   
mount 명령어로 정상적으로 파티션이 생성되어 사용할 수 있는지 확인한다.mount   
   
# mount   
/dev/hda7 on / type ext3 (rw)   
proc on /proc type proc (rw)   
sysfs on /sys type sysfs (rw)   
devpts on /dev/pts type devpts (rw,gid=5,mode=620)   
/dev/hda5 on /home type ext3 (rw)   
/dev/hda3 on /usr type ext3 (rw)   
/dev/hda2 on /var type ext3 (rw)   
/dev/hda1 on /boot type ext3 (rw)   
tmpfs on /dev/shm type tmpfs (rw)   
/dev/hdb5 on /data type ext3 (rw)   
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)   
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)   
#   
