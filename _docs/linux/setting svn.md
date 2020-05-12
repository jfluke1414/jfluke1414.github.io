---
order: 60
title: (LINUX) Setting SVN
category: Linux
---

임포트시,

저장소 만들기
svnadmin create --fs-type fsfs trendup-core


덤프 임포트하기
svnadmin load aa-core < /home/svn/dump/aa-core.dump

svnadmin load aa-core --force-uuid < /home/svn/dump/aa-core.dump

hjyeo = hjyeo


Svn start 명령어
svnserve -d -r /home/svn

------------------------------------------------------------

[1] SVN Repository 생성
명령어 : svnadmin create --fs-type fsfs /home/svn/<REPOSITORY_NAME>
# svnadmin create --fs-type fsfs /home/svn/aaron



[2] SVN Repository 디렉토리 소유자 그룹 변경
# cd /home/svn
# chgrp -R developer aaron



[3] SVN Repository 접근 권한 설정 
(* 기존 생성된 Repository 들의 해당 파일을 참고하여 작성할 것.)
# vi /home/svn/aaron/conf/svnserve.conf 
# vi /home/svn/aaron/conf/passwd



[4] .bash_profile 환경변수 설정
(* 해당 Repository 를 사용할 계정이 따로 존재할 경우에만, 해당 계정의 bash_profile 수정할 것.)
aaron] # vi ~/.bash_profile 
    SVN_EDITOR=/usr/bin/vim
    export SVN_EDITOR



[5] 생성한 SVN Repository 내에 디렉토리 생성
명령어 : svn mkdir svn://<__SERVER_IP>/<REPOSITORY_NAME>/<DIRECTORY_NAME>
# svn mkdir svn://192.168.5.123/aaron/trunk
# svn mkdir svn://192.168.5.123/aaron/branches
# svn mkdir svn://192.168.5.123/aaron/tags
1) :q!
2) C 
3) enter


[6] Repository 체크아웃(Checkout) 하기
(* 서버내 Shell 에서 사용할 경우에만 아래 명령어를 이용하며, 기타 어플리케이션에서는 해당 프로그램의 설정에 맞춰서 체크아웃 수행할 것.)
aaron]# svn checkout svn://192.168.5.123/aaron
A    aaron/trunk
A    aaron/trunk/Hello.c
A    aaron/trunk/Hello.tar
A    aaron/branches
A    aaron/tags
체크아웃된 리비전 4.
