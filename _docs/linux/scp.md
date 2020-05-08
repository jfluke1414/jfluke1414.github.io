---
order: 19
title: (LINUX) scp
category: Linux
---

Scp twitter@destination ip:/home/tter/bin/*.jar .( . 현재 디렉토리 )


(현재 서버에서)
Scp *.jar twitter@destination ip:/home/tter/bin/*.jar


[주의사항]
옵션중에 –P와 –p가 있으니 대/소문자 확인을 하여야 한다.
-P : 포트번호를 지정함
-p : 원본파일 수정/사용시간 및 권한을 유지함
-r : 하위 디렉토리 및 파일 모두 복사함
