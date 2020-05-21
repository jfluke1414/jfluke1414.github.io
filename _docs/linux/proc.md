---   
order: 25   
title: (LINUX) proc   
category: Linux   
---   
   
### error   
[snscrawler@localhost bin]$ ./start.sh    
./start.sh: line 1:  9401 Segmentation fault      pkill -9 java   
Java Process Killed   
Start Cra   
Error, do this: mount -t proc none /proc   
CraStart start   
[snscrawler@localhost bin]$ su -   
   
   
   
### solution   
anaconda-ks.cfg  dkms-2.1.1.2-1.noarch.rpm  install.log  install.log.syslog   
[root@localhost ~]# chmod 755 /proc   
[root@localhost ~]# cd /proc/   
[root@localhost proc]# cd   
[root@localhost ~]# ls   
anaconda-ks.cfg  dkms-2.1.1.2-1.noarch.rpm  install.log  install.log.syslog   
[root@localhost ~]# cd   
[root@localhost ~]# ls   
anaconda-ks.cfg  dkms-2.1.1.2-1.noarch.rpm  install.log  install.log.syslog   
[root@localhost ~]#    
[root@localhost ~]#    
[root@localhost ~]# pwd   
/root   
[root@localhost ~]#    
