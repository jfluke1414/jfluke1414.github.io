---   
order: 100   
title: (LINUX) PHP install - Lltdl error   
category: Linux   
---   
   
### PHP 설치시 다음과 같은 오류 발생시.. 해결방법   
      
/usr/bin/ld: cannot find -lltdl   
collect2: ld returned 1 exit status   
make: *** [libphp5.la] Error 1   
   
#1 첫번 째 해결 방법   
   
yum install libtool-ltdl-devel   
   
이후 다시   
make all   
   
   
위와 같은 명령어를 실행해 libtool-ltdl-devel 를 설치 했음에도 오류가 발생된다면,   
   
#2 두번 째 해결 방법   
   
위와 같은 에러가 발생 시에는 아래와 같이 파일을 수정하도록 합니다.   
$ vi ext/standard/dl.c   
   
수정 전	   
23	#include "php.h"   
24	#include "dl.h"   
아래와 같이 #define HAVE_LIBDL 1 항목을 추가해주면 됩니다.   
   
수정 후	   
23	#define HAVE_LIBDL 1   
24	   
25	#include "php.h"   
26	#include "dl.h"   
이후 다시   
make all   
을 실행하여 컴파일 하니.. 정상적으로 컴파일 된다.   
