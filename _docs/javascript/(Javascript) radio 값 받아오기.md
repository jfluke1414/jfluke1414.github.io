---   
order: 19   
title: (Javascript) radio 값 받아오기   
category: Javascript   
---   
   
```   
var obj = document.getElementsByName("pay_rad");   
alert(obj.length);   
for(var i=0; i<obj.length;i++)   
{   
alert(obj[i].value+" : " + obj[i].checked);   
var temp = obj[i].value   
   
}   
```