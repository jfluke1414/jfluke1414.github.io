---
order: 24
title: Page moving - redirect
category: Javascript
---

Javascript에서 페이지 이동을 하는 방법은 헤드 사이에 다음과 같은 자바스크립트를 넣는 것이다.

이 방법의 핵심은 location.href이다.
<script type='text/javascript'>
<!--
location.href='http://www.example.com/';
//-->
</script>
현재 보여주고 있는 화면의 주소를 http://www.example.com/으로 변경한다는 의미로써,
곧장 http://www.example.com/으로 이동한다.

메타 태그처럼 몇 초 후에 이동하도록 코드를 작성할 수도 있는데 바로 setTimeout을 활용한 방법이다.
<script type='text/javascript'>
<!--
setTimeout("location.href='http://www.example.com/'",5000);
//-->
</script>
setTimeout 함수는 Milisecond단위를 사용하기 때문에 5000은 5초를 뜻한다.
고로 이 코드는 5초 후에 location.href='http://www.example.com'를 실행하라는 의미이다.
여기서 한 가지 중요한 것은 location.href='http://www.example.com'을 둘러싼 큰 따옴표인데,
이것들이 사라지면 5초 후가 아닌 자바스크립트를 읽는 도중에 곧장 실행을 하게 된다.
