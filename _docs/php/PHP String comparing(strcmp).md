---
order: 13
title: PHP String comparing(strcmp)
category: Php
---

php 에서도 문자열 비교함수인 strcmp가 있다. 

strcmp의 경우 일치하는경우 0(false)을, 불일치하는경우 1(true)을 반환한다. 

strcmp
strcmp("문자열1" , "문자열2")

예제 소스 
<?php
$a = "apple";
$b = "apple";
$c = "banana";

$str = strcmp($a, $b);

if($str){
    echo $a . " 와 " . $b ."는 다르다</br>" ;
}else{
        echo $a . " 와 " . $b ."는 같다</br>" ;
}

$str =strcmp($a, $c);
if($str){
    echo $a . " 와 " . $c ."는 다르다</br>" ;
}else{
        echo $a . " 와 " . $c ."는 같다</br>" ;
}
?>




