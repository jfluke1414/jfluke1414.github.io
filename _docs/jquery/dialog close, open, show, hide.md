---
order: 8
title: (Jquery) dialog close, open, show, hide
category: Jquery
---

<cookie 등록(javascript단)>
if ($.cookie('ispopup') != undefined){
    	$( "#main_popup_dialog" ).hide();
    } else {
    	$( "#main_popup_dialog" ).show();
    }

<dialog 닫기(javascript단)>
$( "#main_popup_confirm" ).button().on( "click", function() {
	$( "#main_popup_dialog" ).hide();
});

<하루동안 안보기 check 버튼 닫기(javascript단)>
$( "#exp_popup_chk" ).click (function() {
		if ($("#exp_popup_chk").prop("checked")){
    		$.cookie( 'ispopup', 'false', { path: "/", expires : 1 } );
    		$( "#main_popup_dialog" ).hide();
    	}

	});


<div(view단)>
<!-- Main Popup-->
<div id="main_popup_dialog" >
<style type="text/css">
#main_popup_dialog {
	margin-left: 0px;
	margin-top: 0px;
	margin-right: 0px;
	margin-bottom: 0px;
	position:absolute;
	top:120px;
	width:100%;
}
#main_popup_dialog table{
	margin:0 auto;
}
</style>

<table width="690" border="0" cellspacing="0" cellpadding="0">
    <tr>
      <td><img src="/assets/images/popup/popup01.png" width="690" height="295" alt=""/></td>
    </tr>
    <tr>
      <td bgcolor="#FFFFFF" style="padding-left:40px;"><a href="http://www.isecconference.org/2015/kor/visit/visitor_agree.asp?kind=2&grp=지란지교" target="_blank"><img src="/assets/images/popup/bt01.png" width="214" height="41" alt="" border="0"/></a></td>
    </tr>
    <tr>
      <td><img src="/assets/images/popup/popup02.png" width="690" height="237" alt=""/></td>
    </tr>
    <tr>
      <td height="32" style="background-color:#7c7c7c"><table width="690" border="0" cellspacing="0" cellpadding="0">
          <tr>
            <td width="40" align="right" style="padding-right:3px;"><input type="checkbox" id="exp_popup_chk"/></td>
            <td align="left">&nbsp;<img src="/assets/images/popup/t01.png" width="112" height="32" alt=""/></td>
            <td width="77"><a id="main_popup_confirm"><img src="/assets/images/popup/bt02.png" width="77" height="32" alt=""/></a></td>
          </tr>
      </table></td>
  </tr>
</table>
</div>
