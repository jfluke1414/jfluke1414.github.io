---
title: [APACHE] Apache folder(html) 권한 주기 
category: Linux(setting)
order: 1
---

[root@server177-90 var]# cd var/
[root@server177-90 var]# cd www/
[root@server177-90 www]# ls
cgi-bin  error  html  icons
[root@server177-90 www]# cd html/
[root@server177-90 html]# cd ..
[root@server177-90 www]# ls
cgi-bin  error  html  icons
[root@server177-90 www]# ls -al
합계 28
drwxr-xr-x  6 root root 4096  5월  4 16:31 .
drwxr-xr-x 23 root root 4096  5월  4 16:31 ..
drwxr-xr-x  2 root root 4096  2월  1 07:54 cgi-bin
drwxr-xr-x  3 root root 4096  5월  4 16:31 error
drwxr-xr-x  2 root root 4096  2월  1 07:54 html
drwxr-xr-x  3 root root 4096  5월  4 16:37 icons
[root@server177-90 www]# chown -R apache html
[root@server177-90 www]# pwd
/var/www
