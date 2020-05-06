---
order: 13
title: (Javascript) Image Drobdown시 표시 바꾸기
category: Javascript
---

$(document).ready(function(){
    $(".flip").click(function(){
        $(this).next().slideToggle("slow");
        
        var src = ($(this).find('.penel_icon').attr("src") === "/assets/img/icon07.gif") ? "/assets/img/icon06.gif" : "/assets/img/icon07.gif";
        $(this).find('.penel_icon').attr("src", src); 

    });
});
