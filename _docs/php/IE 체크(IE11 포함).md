---
order: 15
title: IE 체크(IE11 포함)
category: Php
---

if (strpos($_SERVER['HTTP_USER_AGENT'], 'MSIE') !== FALSE ||
    strpos($_SERVER['HTTP_USER_AGENT'], 'Trident') !== FALSE) {
    echo 'You are using Internet Explorer.<br />';
}
