---
order: 25
title: (Javascript) Comparing date
category: Javascript
---


//추가
```
	var now = new Date();
	var today = new Date(now.getFullYear(), now.getMonth(), now.getDate())
	
	selected_date = el.title.replace(/-/gi, '/');
	var specific_date = new Date(selected_date); 

	
	if(today.getTime() > specific_date.getTime()){
		alert("You cannot select past time.");
	} else {
		cal_Day = el.title;
		el.style.borderColor = "red";
		if (cal_Day.length > 7) {
			target.value=cal_Day
		}
		minical.style.display='none';
	}
```