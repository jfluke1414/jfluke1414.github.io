---   
order: 85   
title: (LINUX) Linux telnet 설치   
category: Linux   
---   
   
[root@zetawiki ~]# rpm -qa | grep telnet   
[root@zetawiki ~]# telnet   
-bash: telnet: command not found   
   
[root@zetawiki ~]# yum install telnet   
[root@localhost ~]# rpm -qa | grep telnet   
telnet-0.17-47.el6   
