---
order: 7
title: jQuery, prototype 동시에 사용 시 충돌 해결 방법
category: Jquery
---

javascript 기반으로 개발 할 때 시간을 많이 단축 시켜 주는 유용한 라이브러리 이다. 전역 변수로 같은 $ 를 사용하고 있기 때문에 곂쳐지게 되어 사용이 불가하게 된다.
해결 방법으로는 jQuery 를 먼저 선언 하고 전역 변수명을 바꾸어 주고, prototype 를 선언 한다. 아래 코드를 참고 하자.
<script src="//code.jquery.com/jquery-1.11.2.min.js"></script>
<script src="//code.jquery.com/jquery-migrate-1.2.1.min.js"></script>  
<script type="text/javascript">
jQuery.noConflict();
var w$ = jQuery;
</script>
<script src="https://ajax.googleapis.com/ajax/libs/prototype/1.7.0.0/prototype.js" type="text/javascript"></script>
<script src="https://ajax.googleapis.com/ajax/libs/scriptaculous/1.9.0/scriptaculous.js" type="text/javascript"></script>
위와 같이 변경 하게 되면 라이브러리 선언에 대한 순서에 신경을 써야 한다. jQuery 기반의 라이브러리는 상단에 우선 시 하여 선언 한 후 제일 마지막에 전역 변수명을 변경 하도록 하자.
