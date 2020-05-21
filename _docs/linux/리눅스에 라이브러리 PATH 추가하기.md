---   
order: 77   
title: (LINUX) 리눅스에 라이브러리 PATH 추가하기   
category: Linux   
---   
   
리눅스에 라이브러리 경로를 추가하고 싶을 때..   
2가지 방법이 있다.   
   
첫 번재는 /etc/ld.so.conf 파일에 경로를 입력하는 것( path : /usr/local/lib )   
include /usr/local/lib   
입력 후 ldconfig 로 다시 링킹 정보를 읽는다.   
   
두 번째는 /etc/profile 에 입력하는 것   
LD_LIBRARY_PATH=/usr/local/lib   
export LD_LIBRARY_PATH   
입력 후 재로그인을 해줘야 한다.   
