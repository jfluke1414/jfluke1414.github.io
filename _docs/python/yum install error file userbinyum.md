---                  
order: 12   
title: (Python) yum install error file userbinyum  
category: Python   
---   
   
yum is depending on python 2.*.   
If you use python 3.*   
have to change the link.   

### command   
1. cd /usr/bin   
2. ls -al | grep python   
3. ln -s python2.7 python   

rm link_name   
ex)rm python   

4. yum install cmake   
when I tried to install mysql, there was an error as cmake does not work.      