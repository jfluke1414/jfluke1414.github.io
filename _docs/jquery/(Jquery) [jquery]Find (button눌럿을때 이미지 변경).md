---
order: 4
title: [jquery]Find (button눌럿을때 이미지 변경)
category: Jquery
---

var src = ($(this).find('.penel_icon').attr("src") === "/assets/img/icon07.gif") ? "/assets/img/icon06.gif" : "/assets/img/icon07.gif";

        $(this).find('.penel_icon').attr("src", src); 