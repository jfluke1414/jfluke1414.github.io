---
order: 9
title: (PHP) Check Email
category: Php
---

if( filter_var($user_email, FILTER_VALIDATE_EMAIL) == ""){
			$msg = "Email을 확인해주세요.";
			echo("<script>alert('$msg');history.back();</script>");
			exit;
		}


