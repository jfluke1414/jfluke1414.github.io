---
order: 20
title: Get Date
category: Javascript
---

var now_date = Date();
	var date = new Date();
	
	var year_date = date.getFullYear();
	var month_date = date.getMonth()+1;
	var day_date = date.getDate();
	var hour_date = date.getHours();
	var minute_date = date.getMinutes();

	if(month_date.toString().length == 1) month_date = "0"+month_date;
	if(day_date.toString().length == 1) day_date = "0"+day_date;
	var total_date = year_date+""+month_date+""+day_date+""+hour_date+""+minute_date;

	

	if(term == 1){
		month_date = date.getMonth()+1;
		total_date = year_date+""+month_date+""+day_date+""+hour_date+""+minute_date;
	}
	if(term == 3){
		month_date = date.getMonth()+4;
		total_date = year_date+""+month_date+""+day_date+""+hour_date+""+minute_date;
	}
	if(term == 6){
		month_date = date.getMonth()+7;
		total_date = year_date+""+month_date+""+day_date+""+hour_date+""+minute_date;
	}
	if(term == 12){
		year_date = date.getFullYear()+2;
		total_date = year_date+""+month_date+""+day_date+""+hour_date+""+minute_date;
	}
	
	
	alert(total_date);
