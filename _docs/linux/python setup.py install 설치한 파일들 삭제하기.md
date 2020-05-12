---
order: 86
title: (LINUX) python setup.py install 설치한 파일들 삭제하기
category: Linux
---

1. 다시 설치하는데 –record 옵션을 줘서 기록한다.
$ python setup.py install --record uninstall.txt
2. 설치한 파일을 하나씩 삭제한다.

cat uninstall.txt | xargs rm -rf
