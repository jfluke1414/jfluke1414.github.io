---
order: 35
title: (LINUX) du
category: Linux
---

1. 기능
du 는 Disk Usage를 의미하며, 지정된 디렉토리의 디스크 사용량을 표시해준다.
2. 문법 
# du [옵션] 파일
3. 옵션
-a : 디렉토리가 아닌 모든 파일에 대한 정보를 출력
-k : 결과 값을 KB 단위로 출력한다. (기본값)
-m : 결과 값을 MB 단위로 출력한다.
-h : 사용자가 이해하기 쉬운 용량의 단위를 표시한다. ((ex) KB,MB,GB)
-l : 하드 링크의 용량을 모두 계산한다. 
-s : 사용량의 총 합계만 출력한다. 
-S : 하위 디렉토리를 합치지 않고, 각각을 나누어서 계산한다.
지정된 디렉토리 내의 파일과 모든 하위 디렉토리의 용량, 내용까지 볼 수 있다.
4. 사용방법 및 정보
가) home 디렉토리 내의 사용량의 총합을 알아보기 쉬운 단위로 표시한다.

[root@sense tar]# du -sh /home
484K /home
나) home 디렉토리내에 있는 모든 디렉토리와 파일들의 정보를 표시한다.

[root@sense tar]# du -a /home
8 /home/lebowski/.zshrc
8 /home/lebowski/.gtkrc
------------중략----------------- 
56 /home/linuxone
484 /home

