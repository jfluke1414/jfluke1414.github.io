---   
order: 1   
title: (Jquery) Tree menu(dropdown)   
category: Jquery   
---   
   
```   
<link href="/assets/css/menu.css" rel="stylesheet" type="text/css" />   
<script type="text/javascript">   
	$(document).ready(function() {   
		$('.myMenu > li').bind('mouseover', openSubMenu);   
		$('.myMenu > li').bind('mouseout', closeSubMenu);   
		   
		function openSubMenu() {   
			$(this).find('ul').css('visibility', 'visible');	   
		};   
		   
		function closeSubMenu() {   
			$(this).find('ul').css('visibility', 'hidden');	   
		};   
				      
	});   
</script>   
   
<div style="margin-bottom:60px";>   
	<ul class="myMenu" style="">   
		<li><a href="/manage/manager_list">계정관리</a></li>   
		<li><a href="#">게시판관리↓</a>   
			<ul>   
				<li><a href="/manage/lists/1">공지사항</a></li>   
				<li><a href="/manage/lists/2">주의사항</a></li>   
				<li><a href="/manage/lists/3">이용문의</a></li>   
			</ul>   
		</li>   
		<li><a href="#">서비스↓</a>   
			<ul>   
				<li><a href="/manage/inspect">신청현황</a></li>   
				<li><a href="/manage/inspect_all">전체내역</a></li>   
			</ul>   
		</li>   
		<li><a href="#">발송 관리↓</a>   
			<ul>   
				<li><a href="/manage/template">템플릿관리</a></li>   
				<li><a href="/manage/report_mailing">리포트 메일 발송</a></li>   
				<li><a href="/manage/report_sendlist">리포트 발송 내역</a></li>   
			</ul>   
		</li>   
		<li><a href="#">과금↓</a>   
			<ul>   
				<li><a href="/manage/receipt">과금내역</a></li>   
				<li><a href="/manage/userlist">사용자내역</a></li>   
			</ul>   
		</li>   
	</ul>   
</div>   
```