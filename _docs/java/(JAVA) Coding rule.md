---
order: 4
title: (JAVA) Coding rule
category: Java
---

● 주석 shift+Alt+j  : Export -> javadoc 설정 하위 폴더 class file 저장

● Import   java.util.regex.pattern  처럼 하나씩 import를 시켜준다.

● 배열을 검색하여 줄때
	String[] data = {"","",""};
	For(int i=0; i<data.length; i++)
	보다
	For(String keyword : data) 방법으로
	간단하고 심플하게!!
	배열 data의 속성들이 String keyward로 모두 저장된다.
