---
order: 8
title: (JAVA) Singlton
category: Java
---

1. Singleton 패턴 
```
2. class Singleton { 
3. private static Singleton instance;
4. private Singleton(){ 
5. } 
6. public static Singleton getInstance(){ 
7. if (instance == null) 
8. instance = new Singleton();  
9. return instance; 
10. } 
11. }
```
