---                     
order: 106   
title: (LINUX) SVN setting   
category: Linux                     
---                     
                     
### Install SVN    
   
## 1. Create SVN user   
adduser svn   
passwd svn   
   
## 2. SVN 생성   
svnadmin create --fs-type fsfs /home/svn/crypto   
   
## 3. 그룹 소유자 변경   
cd /home/svn   
chown -R svn:svn /home/svn/crypto   
chown -R root:root /home/svn/crypto   
   
## 4. 설정파일 수정   
vi /home/svn/crypto/conf/svnserve.conf   
# 익명 사용자 읽기 사용 여부   
anon-access = read   
# 인증 사용자 쓰기 사용 여부   
auth-access = write   
# 인증에 사용될 패스워드 설정 파일   
password-db = passwd   
   
## 5. Start   
svnserve -d -r /home/svn/   
   
- check service   
ps -aux | grep svn   
   
## 6. bash_profile 수정   
vi ~/.bash_profile?   
   
추가/수정   
SVN_EDITOR=/usr/bin/vi   
export SVN_EDITOR   
   
source .bash_profile   
   
## 7.   
svn mkdir svn://13.58.191.130/crypto/trunk   
svn mkdir svn://ec2-13-58-191-130.us-east-2.compute.amazonaws.com/crypto/trunk   
   
svn mkdir svn://13.58.191.130/crypto/branches   
svn mkdir svn://13.58.191.130/crypto/tags   
   
1) :q!   
2) C    
3) enter   
   
   
## 8. checkout   
svn checkout svn://ec2-13-58-191-130.us-east-2.compute.amazonaws.com/crypto   
   
   
### eclipse   
help -> install software   
add   
   
name : svn   
location : http://subclipse.tigris.org/update_1.10.x   
