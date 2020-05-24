---                  
order: 105      
title: (LINUX) memory swap setting   
category: Linux                  
---                  
                  
### Memory swap 늘리기   
   
## 1.do things below in order   
fallocate -l 1GB /swapfile   
sudo dd if=/dev/zero of=/swapfile count=1024 bs=1MiB   
   
chmod 600 swapfile   
mkswap /swapfile   
swapon /swapfile   
free -m   
