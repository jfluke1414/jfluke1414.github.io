---
order: 1
title: (JAVA) Interface
category: Java
---

추상클래스를 부분적으로만 완성된 '미완성 설계도'라고 한다면, 인터페이스를 구현된 것은
아무것도 없고 밑그림만 그려져 있는 '기본 설계도'라 할 수 있다.
 인터페이스도 추상클래스처럼 완성되지 않은 불완전한 것이기 때문에 그 자체만으로 사용되기 보다는
다른 클래스를 작성하는데 도움 줄 목적으로 작성된다.

### 사용방법
인터페이스를 작성하는 것은 클래스를 작성하는 것과 같다. 다만 키워드로 class 대신 interface를 사용한다는 것만 다르다. 그리고 interface에도 클래스와 같이 접근제어자로 public 또는 default를 사용할 수 있다.

```
 public interface hyunjin{

 public void jin(){

	}
}
```

상속 받아 쓸려면
```
Class inzaghi implements hyunjin{
	Public void jin(){   // 추상메서드를 하나 가지게 된다.
	
	}
}
```

