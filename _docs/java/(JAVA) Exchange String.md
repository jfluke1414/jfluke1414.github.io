---
order: 14
title: (JAVA) Exchange String
category: Java
---

### ◆ 숫자의 문자열 변환(C에서 itoa 함수) 
int a=1000; String s=””+a; 정수 a를 문자열로 변환 
String s1 = “”+3.141592; 부동 소수 3.141592를 문자열로 변환 
String s1 = “”+0; 정수 0을 문자열로 변환 

### ◆ 문자열의 숫자 변환 
Byte.parseByte(“123”) ‘123’을 바이트형 정수로 변환 
Short.parseShort(“123”) ‘123’을 short형 정수로 변환 
Integer.parseInteger(“123”) ‘123’을 int형 정수로 변환 
Long.parseLong(“123”) ‘123’을 long형 정수로 변환 
Float.parseFloat(“123”) ‘123’을 float형 부동 소수로 변환 
Double.parseDouble(“123”) ‘123’을 double형 부동 소수로 변환 

### ◆ 문자열 상수를 이용한 안전한 equals 메쏘드 
·”Park”.equals(name) : “Park”와 같은 문자열 리터럴은 내부적으로 스트링 객체로 표현되므로, String 클래스에서 제공하는 메쏘드 사용 가능 
·name.equals(“Park”) : name이 null일 경우, NullPointerException 발생 가능(자바는 내부적으로 유니코드를 사용하기 때문) 
“Park”.length() --> 4 
“박용우”.length() --> 3 
·문자열의 실제 길이 구하기(바이트 배열로 얻은 후 구함) 
“Park”.getBytes().length --> 4 
“박용우”.getBytes().length --> 6 
