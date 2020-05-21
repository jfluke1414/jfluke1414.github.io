---   
order: 80   
title: (LINUX) [LINUX]Nmon(so good)   
category: Linux   
---   
   
sudo su   
   
### Download NMON archive   
   
cd /tmp   
   
wget http://nmon.sourceforge.net/docs/MPG_nmon_for_Linux_14a_binaries.zip   
   
### Install unzip if you don't have   
   
yum install unzip   
   
### Unzip archive   
   
unzip MPG_nmon_for_Linux_14a_binaries.zip   
   
### Copy nmon file   
   
cp nmon_x86_64_centos5 /usr/local/bin/   
   
chmod a+x /usr/local/bin/nmon_x86_64_centos5   
   
### Create symbolic link   
   
ln -s /usr/local/bin/nmon_x86_64_centos5 /usr/local/bin/nmon   
