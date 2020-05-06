---
title: Oracle Data 흐름(구조)
category: Oracledb
order: 2
---

Data를 insert하게 되면
Data가 저장이 되고 logbuffer에 binary 형태로 두 가지가 저장이 된다.
만약에 logbuffer가 다 차게 되면
다음은 디스크에 저장을 하게 되는데 
디스크가 256MB이고 디스크가 5개가 있으면 순차적으로 
디스크를 채우게 된다. 이것을 read log라 한다.
Read log가 다 차게 되면 아카이브 로그에 logbuffer에 있던 디렉토리, log등을 복사해서 채우게 된다.
이러한 특히 insert, update의 양이 많을 경우에는 속도에 문제가 많다.
백만건인 경우 대체로 괜찮지만 천만건, 억만건인 경우에는 속도가 현저히 떨어진다.

대처방안으로 이 로그들을 메모리에 저장하게 하면 속도는 빠르지만
정전들이 되었을 경우 log들이 다 날아가 복구를 하지 못하는 치명성이 있다.
