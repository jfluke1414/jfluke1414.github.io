---
order: 11
title: Get date before a year
category: Php
---

$now_date = date("YmdHi");
$date = new DateTime($now_date);
$date->modify('+1 year');
$future_date = $date->format('YmdHi');


