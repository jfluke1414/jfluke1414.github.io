---
order: 10
title: (PHP-codeig) Auto link a (codeig, php, html)
category: Php - codeignitor
---

※ 반드시 str_replace Array 사용 해야함. ※ 
//controller
$content = str_replace(array("\r\n", "\r", "\n"), '<br/>', $content);
$content = str_replace(array(" "), '&nbsp;', $content);
$content = auto_link($content, 'url', true);
$replied_content = str_replace(array("\r\n", "\r", "\n"), '<br/>', $replied_content);
$replaced_content = str_replace(array(" "), '&nbsp;', $replied_content);
$replied_content = auto_link($replied_content, 'url', true);


//html
$content = $list->content;
$content = str_replace(array("\r\n", "\r", "\n"), '<br/>', $content); // 엔터
$content = str_replace(array(" "), '&nbsp;', $content); //스페이스
$content = auto_link($content, 'url', true); // a link
$content = str_replace(array(";"), '', $content); 


//예외사항
$content = $list->content;
$content = str_replace(array("\r\n", "\r", "\n"), '<br/>', $content);
$content = str_replace(array(" "), '&nbsp;', $content);
$content = auto_link($content, 'url', true);
$content = str_replace(array(";"), '', $content);
$content = str_replace(array("&nbsp"), ' ', $content);

