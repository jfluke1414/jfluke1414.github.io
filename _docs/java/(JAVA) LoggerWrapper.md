---
order: 6
title: (JAVA) LoggerWrapper
category: Java
---

LoggerWrapper.debug("syndiplus-rule-downloader", e)
LoggerWrapper.debug("syndiplus-rule-downloader", "DownComplete")
LoggerWrapper.debug("syndiplus-rule-downloader", "")

System.exit(1);

LoggerWrapper은 스레드로 돌아가기 때문에 강제로 종료를 해줘야 한다.
LoggerWrapper. 자동으로 닫아주는 메소드가 없다.
