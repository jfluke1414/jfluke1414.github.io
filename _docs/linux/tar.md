---
order: 15
title: (LINUX) tar
category: Linux
---

compression
.tar로 파일 묶기~
tar cvf <파일명.tar> <압축할 폴더명>
.tgz나 .tar.gz로 파일 압축하기~
tar cvfz <파일명.tar.gz> <압축할 폴더명>
tar cvfz <파일명.tgz> <압축할 폴더명>

extraction
확장자가 .tar 로 압축된 파일 풀기~ 
tar xvf <파일명>
확장자가 .tgz나 .tar.gz일 때 tar 명령어로 압축 풀기~
tar xvfz <파일명>

먼저 tar의 옵션을 알아보겠습니다
-c 파일을 tar로 묶음
-p 파일 권한을 저장
-v 묶거나 파일을 풀때 과정을 출력
-f 파일이름을 지정

-C 경로를 지정
-x tar 압축풀기
-z gzip으로 압축하거나 해제함
자주 사용하는 옵션들 입니다 ㅎㅎ

그럼 압축 명령어를 알아보겠습니다

-그냥 tar으로 압축하기
tar -cvf (압축 파일명).tar (압축할 폴더 또는 파일)

-tar.gz로 압축하기
tar -zcvf (압축될 이름.tar.gz) (압축할 폴더/파일)

-tgz로 압축하기
tar -zcvf (압축될 이름.tgz) (압축할 폴더/파일)


그럼 이번에는
압축 풀기 명령어를 알아보겠습니다

-tar 압축풀기
tar -xvf (압축파일명).tar

-tar.gz 압축풀기
tar -xvzf (압축파일명).tar.gz

-tgz 압축풀기
tar -xzvf (압축파일명).tgz
