---
order: 3
title: (Ajax) ajax에서 input 태그안의 value 에 값넣기
category: Ajax
---

var enc = "값";
$('input[name=enc]').attr('value',enc); 
input 으로 설정한 태그 안의 name 이 enc 인 곳에 

value 를 enc변수의 값으로 설정하는 부분

<input type="text" name="enc" value=""/>
결과적으로 위 태그에서
<input type="text" name="enc" value="enc"/> 태그로 변경 된다. 
