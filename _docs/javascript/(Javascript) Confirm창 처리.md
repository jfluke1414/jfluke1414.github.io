---
order: 17
title: (Javascript) Confirm창 처리
category: Javascript
---

function delete_user_Function(){
	
	var answer = confirm('정말 탈퇴하시겠습니까?')
	if(!answer){
		return false;
	}
	return true;
}

