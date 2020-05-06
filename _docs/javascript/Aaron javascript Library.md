---
order: 15
title: Aaron javascript Library
category: Javascript
---

function newPopup(url) {
	popupWindow = window.open(
		url,'popUpWindow','height=700,width=800,left=10,top=10,resizable=yes,scrollbars=yes,toolbar=yes,menubar=no,location=no,directories=no,status=yes')
}

function change_fileExt(value){
	<!--document.getElementById('file_ext').value= document.getElementById('upload_file').files[0].name;-->
	document.getElementById('change_file_ext').innerHTML = document.getElementById('change_file').files[0].name;
}

function upload_fileExt(value){

	document.getElementById('upload_file_ext').innerHTML = document.getElementById('upload_file').files[0].name;
	
}

function upload_Certifi_Ext(value){

	document.getElementById('upload_certifi_ext').innerHTML = document.getElementById('upload_certifi').files[0].name;
	
}

function change_Certifi_Ext(value){

	document.getElementById('change_certifi_ext').innerHTML = document.getElementById('change_certification_file').files[0].name;
	
}

function partner_loginFunction() {
	      
	var mailformat = /^([a-zA-Z0-9_\.\-])+\@(([a-zA-Z0-9\-])+\.)+([a-zA-Z0-9]{2,4})+$/;
	var username = document.getElementById('username').value;
	
	
	if(!username.match(mailformat))  
	{  
		alert("Enter a Email account ID");
		return false;  
	}  
	
}



function forget_loginFunction() {
    
	var mailformat = /^([a-zA-Z0-9_\.\-])+\@(([a-zA-Z0-9\-])+\.)+([a-zA-Z0-9]{2,4})+$/;
	var username = document.getElementById('forget_userid').value;
	
	if(!username.match(mailformat))  
	{  
		alert("Enter a Email account ID");
		return false;  
	}  
	
}



$(document).ready(function(){
	var isFist = false;
	
    $(".flip").click(function(){
        $(this).next().slideToggle("slow");
        
        if(isFist == false){
	        var src = ($(this).find('.penel_icon').attr("src") === "/assets/img/icon06.gif") ? "/assets/img/icon07.gif" : "/assets/img/icon06.gif";
	        $(this).find('.penel_icon').attr("src", src);
	        isFirst = true;
        } else {
        	var src = ($(this).find('.penel_icon').attr("src") === "/assets/img/icon07.gif") ? "/assets/img/icon06.gif" : "/assets/img/icon07.gif";
	        $(this).find('.penel_icon').attr("src", src); 	
        }
        

      });
});


function Add_UserFunction() {
	var add_userid = document.getElementById('add_userid').value;
	var add_userpw = document.getElementById('add_userpw').value;
	var add_username = document.getElementById('add_username').value;
	var add_useremail = document.getElementById('add_useremail').value;
	var add_partner = document.getElementById('add_partner').value;
	var add_phone = document.getElementById('add_phone').value;
	var add_country = document.getElementById('add_country').value;
	var add_product = document.getElementById('add_product').value;
	var add_remarks = document.getElementById('add_remarks').value;
	
	   	
	if(add_userid == ''){
		alert("Please enter the ID.");
		return false;

	}if(add_userpw == ''){
		alert("Please enter the PW.");
		return false;
	}if(add_username == ''){
		alert("Please enter the UserName.");
		return false;
	}if(add_useremail == ''){
		alert("Please enter the Email.");
		return false;
	}if(add_partner == ''){
		alert("Please enter the Partner.");
		return false;
	}if(add_phone == ''){
		alert("Please enter the Phone number.");
		return false;
	}if(add_country == ''){
		alert("Please enter the Conutry.");
		return false;
	}if(add_product == ''){
		alert("Please enter the Product.");
		return false;
	}
	return true;
}

function support_onlineFunction() {
	var checkbox = document.getElementById('checkbox').value;
	var support_online_text = document.getElementById('support_online_text').value;
	   	
	if(support_online_text == ''){
		alert("Please input the contents.");
		return false;

	}if(!checkbox){
		alert("Please select the category.");
		return false;
	}
	return true;
}

function admin_faqFunction() {
	var checkbox = document.getElementById('checkbox').value;
	var admin_faq_title = document.getElementById('admin_faq_title').value;
	var admin_faq_text = document.getElementById('admin_faq_text').value;
	 
	if(admin_faq_title == ''){
		alert("Please enter the title.");
		return false;

	}  	
	if(admin_faq_text == ''){
		alert("Please input the contents.");
		return false;

	}if(!checkbox){
		alert("Please select the category.");
		return false;
	}
	return true;
}


function uploadCertiFunction() {
	var upload_certifi = document.getElementById('upload_certifi').value;
	   	
	if(!upload_certifi){
		alert("Please select the file.");
		return false;
	}
	return true;
}


function changeCertifiFunction() {
	var change_certification_file = document.getElementById('change_certification_file').value;
	   	
	if(!change_certification_file){
		alert("Please select the file.");
		return false;
	}
	return true;
}


function uploadFunction() {
	var version = document.getElementById('upload_version').value;
	var upload_file = document.getElementById('upload_file').value;
	   	
	if(version == ''){
		alert("Please input the version.");
		return false;

	}if(!upload_file){
		alert("Please select the file.");
		return false;
	}
	return true;
}
	
function upload_changeFunction() {
	var version = document.getElementById('change_version').value;
	var upload_file = document.getElementById('change_file').value;
	   	
	if(version == ''){
		alert("Please input the version.");
		return false;

	}if(!upload_file){
		alert("Please select the file.");
		return false;
	}
	return true;
}


function change_pwFunction() {
	var oldpw = document.getElementById('oldpw').value;
	var newpw1 = document.getElementById('newpw1').value;
	var newpw2 = document.getElementById('newpw2').value;
	
	   	
	if(oldpw == '' || newpw1 == '' || newpw2 == ''){
		alert("All category is required to fill up.");
		return false;

	}if(newpw1 != newpw2){
		alert("New password does not match.");
		return false;
	}
	return true;
}
	

$(function() {
	
	  var select_id;
    
	    dialog_common = $( "#dialog_common" ).dialog({
	      autoOpen: false,
	      height: 800,
	      width: 525,
	      modal: true,
	      resizable: true,
		  draggable: true,
		  
	    });
	  
	  
	    dialog = $( "#dialog-form" ).dialog({
	      autoOpen: false,
	      height: 440,
	      width: 590,
	      modal: true,
	      resizable: false,
		  draggable: true,
		  
	    });
	 	
	 	user_reply_dialog = $( "#user_reply_dialog" ).dialog({
	      autoOpen: false,
	      height: 590,
	      width: 525,
	      modal: true,
	      resizable: false,
		  draggable: true,
		  
	    });
	    
	    admin_request_replied_dialog = $( "#admin_request_replied_dialog" ).dialog({
	      autoOpen: false,
	      height: 590,
	      width: 525,
	      modal: true,
	      resizable: false,
		  draggable: true,
		  
	    });
	    
	    admin_request_reply_dialog = $( "#admin_request_reply_dialog" ).dialog({
	      autoOpen: false,
	      height: 590,
	      width: 525,
	      modal: true,
	      resizable: false,
		  draggable: true,
		  
	    });
	 	
	 	admin_doc_change_dialog = $( "#admin_doc_change_dialog" ).dialog({
	      autoOpen: false,
	      height: 380,
	      width: 525,
	      modal: true,
	      resizable: false,
		  draggable: true,
		  
	    });
	 	
	 	admin_doc_upload_dialog = $( "#admin_doc_upload_dialog" ).dialog({
	      autoOpen: false,
	      height: 380,
	      width: 525,
	      modal: true,
	      resizable: false,
		  draggable: true,
		  
	    });
	    
	    
	    admin_management_dialog = $( "#admin_management_dialog" ).dialog({
	      autoOpen: false,
	      height: 790,
	      width: 525,
	      modal: true,
	      resizable: false,
		  draggable: true,
		  
	    });
	    
	    
	    admin_popup_edit_dialog = $( "#admin_popup_edit_dialog" ).dialog({
	      autoOpen: false,
	      height: 590,
	      width: 525,
	      modal: true,
	      resizable: false,
		  draggable: true,
		  
	    });
	    
	    user_forgetpw_dialog = $( "#user_forgetpw_dialog" ).dialog({
	      autoOpen: false,
	      height: 590,
	      width: 525,
	      modal: true,
	      resizable: false,
		  draggable: true,
		  
	    });
	    
	 	
	    //Close
	    $( "#reply_close" ).button().on( "click", function() {
	    	user_reply_dialog.dialog( "close" );
	    });
	    
	    
	    $( "#admin_request_replied_close" ).button().on( "click", function() {
	    	admin_request_replied_dialog.dialog( "close" );
	    });
	    
	    
	    $( "#admin_request_reply_close" ).button().on( "click", function() {
	    	admin_request_replied_dialog.dialog( "close" );
	    });
	    
	    $( "#admin_faq_edit_close" ).button().on( "click", function() {
	    	dialog_common.dialog( "close" );
	    });

        
	    //admin_upload_file
	    $( "#admin_upload_file" ).button().on( "click", function() {
	    	
			var form_data = new FormData($("#uploadForm").serialize());
            var files = $("#upload_file").get(0).files;

			if (files.length > 0) {
            	form_data.append("uploadfile", files[0]);
            }
            
            
            postData = $(this).attr("upload_file");
            
	        $.ajax({
	            type        : "POST",
	            url         : "/admin/uploadFile",
	            dataType    : "json",
	            data : postData,
                processData: false,
                
			    success : function(data){
			    	if(data.status == "success"){
			    		alert(data.message);
			    		admin_request_reply_dialog.dialog( "close" );
	
			    	} else if(data.status == "error"){
			    		alert(data.message);
			    	}
			    },
			    error : function(results){
		            alert(results.message);
			    }   
	        })
	      
	    });
	    
	    
	    //admin_management_save
	    $( "#admin_management_save" ).button().on( "click", function() {
			admin_management_dialog.dialog( "open" );
	    });
	    
	    	 	
	 	//Open
	    $( ".change_pw" ).button().on( "click", function() {
	      dialog.dialog( "open" );
	    });


		//admin_certifi_upload
	    $( ".admin_certifi_upload" ).button().on( "click", function() {
	    	
	    	var post_id = $(this).attr("data");
	    	var post_product = $(this).attr("data1");
			var dataString = 'post_id='+ post_id + '&post_product='+ post_product;
			
	        $.ajax({
	            type        : "POST",
	            url         : "/admin/upload_view",
	            data        : dataString,  
	            dataType    : "json",
	            encode      : true,

			    success : function(data){
			    	
			    	if(data.status == "success"){
			    		
			    		admin_doc_upload_dialog.dialog( "open" );
			    		$('#select_upload_id').val(data.id);
			    		$('#select_upload_product').val(data.product);
			    	}

			    },
			    error : function(results){
		            alert(results.message);
			    }   
	        })
	      
	    });


		//admin_user_delete
	    $( ".admin_user_delete" ).button().on( "click", function() {
	    	
	    	var post_id = $(this).attr("data");
			var dataString = 'post_id='+ post_id;
			
	        $.ajax({
	            type        : "POST",
	            url         : "/admin/del_user",
	            data        : dataString,  
	            dataType    : "json",
	            encode      : true,

			    success : function(data){
			    	
			    	if(data.status == "success"){
			    		alert(data.message)
			    		window.location.reload();
			    	}
			    },
			    error : function(results){
		            alert(results.message);
			    }   
	        })
	    });	   
	    
	    
		//admin_certifi_delete
	    $( ".admin_certifi_delete" ).button().on( "click", function() {
	    	
	    	var post_id = $(this).attr("data");
	    	var post_product = $(this).attr("data1");
	    	var post_path = $(this).attr("path");
	    	var post_filename = $(this).attr("filename");
			var dataString = 'post_id='+ post_id + '&post_product='+ post_product + '&post_path='+ post_path + '&post_filename='+ post_filename;
			
	        $.ajax({
	            type        : "POST",
	            url         : "/admin/del_certifi",
	            data        : dataString,  
	            dataType    : "json",
	            encode      : true,

			    success : function(data){
			    	
			    	if(data.status == "success"){
			    		alert(data.message)
			    		window.location.reload();
			    	}
			    },
			    error : function(results){
		            alert(results.message);
			    }   
	        })
	    });	   
	   

	    //admin_doc_upload
	    $( ".admin_doc_upload" ).button().on( "click", function() {
	    	
	    	var post_id = $(this).attr("data");
			var dataString = 'post_id='+ post_id;
			
	        $.ajax({
	            type        : "POST",
	            url         : "/admin/upload_view",
	            data        : dataString,  
	            dataType    : "json",
	            encode      : true,

			    success : function(data){
			    	
			    	if(data.status == "success"){
			    		
			    		admin_doc_upload_dialog.dialog( "open" );
			    		$('#select_upload_id').val(data.id);
			    	}

			    },
			    error : function(results){
		            alert(results.message);
			    }   
	        })
	      
	    });
	    
	    
	    
	    //admin_doc_change
	    $( ".admin_doc_change" ).button().on( "click", function() {
	    	
	    	var post_id = $(this).attr("data");
			var dataString = 'post_id='+ post_id;
			
	        $.ajax({
	            type        : "POST",
	            url         : "/admin/change_view",
	            data        : dataString,  
	            dataType    : "json",
	            encode      : true,

			    success : function(data){
			    	
			    	if(data.status == "success"){
			    		
			    		admin_doc_change_dialog.dialog( "open" );

			    		$('#admin_doc_change_filename').text(data.filename);
			    		$('#select_change_filename').val(data.filename);
			    		$('#select_change_filepath').val(data.path);
			    		$('#select_change_id').val(data.id);

			    	}

			    },
			    error : function(results){
		            alert(results.message);
			    }   
	        })
	      
	    });
	    
	    
	    
	    //admin_edit_save
	    $( "#admin_edit_save" ).button().on( "click", function() {
	    	
	    	id = $("#admin_edit_id").text();
	    	content = $("#edit_replied_content").html();

			var dataString = 'post_id='+ id + '&post_content='+ content;
			alert(dataString);
	        $.ajax({
	            type        : "POST",
	            url         : "/admin/edit_update",
	            data        : dataString,  
	            dataType    : "json",
	            encode      : true,

			    success : function(data){
			    	
			    	if(data.status == "success"){
			    		alert(data.message);
			    		admin_popup_edit_dialog.dialog( "close" );
			    		admin_request_replied_dialog.dialog( "close" );
						window.location.reload();
			    	} else if(data.status == "error"){
			    		alert(data.message);
			    	}

			    },
			    error : function(results){
		            alert(results.message);
			    }   
	        })
	      
	    });
	    
	    	 
	    //admin_request_replied_edit
	    $( "#admin_request_replied_edit" ).button().on( "click", function() {
	    	
	    	var post_thread = $(this).attr("data");
			var dataString = 'post_thread='+ post_thread;
			
			content = $("#request_content").html();
			date = $("#request_date").text();
			category = $("#request_category").text();
			
			
			replied_content = $("#request_replied_content").html();
			replied_id = $("#request_replied_id").text();
			
			admin_popup_edit_dialog.dialog( "open" );
			
			$("#edit_replied_content").html(replied_content.replace(/<br>/g,"\n"));
			
			$("#admin_edit_date").html(date);
			$("#admin_edit_category").html(category);			
			$("#admin_edit_content").html(content);
			$("#admin_edit_id").val(replied_id);

	    });	
	    
	    
	    //admin_faq_edit
	    $( ".admin_faq_edit" ).button().on( "click", function() {
	    	
	    	
	    	var faq_id = $(this).attr('faq_id');
	    	var faq_category = $(this).attr('faq_category');
	    	var faq_title = $(this).attr('faq_title');
			var faq_content = $(this).attr('faq_content');
			var faq_date = $(this).attr('faq_date');
			
			dialog_common.dialog( "open" );
			
			$("#edit_faq_id").text(faq_id);
			$("#edit_faq_category").html(faq_category);
			$("#edit_faq_title").val(faq_title);
			
			var content = faq_content.replace(/<br\/>/g,"\n");
			
			$("#edit_faq_content").val(content);
			$("#edit_faq_date").html(faq_date);
			
			$("#hid_edit_faq_id").val(faq_id);

	    });	
	    
	    
	  //admin_faq_delete
	    $( ".admin_faq_delete" ).button().on( "click", function() {
	    	
	    	var post_id = $(this).attr("data");
			var dataString = 'post_id='+ post_id;
			
	        $.ajax({
	            type        : "POST",
	            url         : "/admin/del_faq",
	            data        : dataString,  
	            dataType    : "json",
	            encode      : true,

			    success : function(data){
			    	
			    	if(data.status == "success"){
			    		alert(data.message);
			    		window.location.reload();
			    	}

			    },
			    error : function(results){
		            alert(results.message);
			    }   
	        })
	    });
	    
	    
   	    //admin_request_reply_save
	    $( "#admin_request_reply_save" ).button().on( "click", function() {
	    	
	    	id = $("#admin_request_reply_id").text();
	    	depth = $("#admin_request_reply_depth").text();
	    	content = $("#admin_request_reply_text").val();
			category = $("#admin_request_reply_category").text();
			
			var dataString = 'post_id='+ id + '&post_depth='+ depth+ '&post_content='+ content+ '&post_category='+ category;

	        $.ajax({
	            type        : "POST",
	            url         : "/admin/save_answer",
	            data        : dataString,  
	            dataType    : "json",
	            encode      : true,
			    success : function(data){
			    	
			    	if(data.status == "success"){
			    		alert(data.message);
			    		admin_request_reply_dialog.dialog( "close" );
						window.location.reload();
			    	} else if(data.status == "error"){
			    		alert(data.message);
			    	}
			    },
			    error : function(results){
		            alert(results.message);
			    }   
	        })
	      
	    });
	    

	    
	    //admin request reply
	    $( ".admin_request_Reply" ).button().on( "click", function() {
	    	
	    	var post_id = $(this).attr("data");
			var dataString = 'post_id='+ post_id;

	        $.ajax({
	            type        : "POST",
	            url         : "/admin/Reply_getList",
	            data        : dataString,  
	            dataType    : "json",
	            encode      : true,
			    success : function(data){
			    	
			    	if(data.status == "success"){
			    		admin_request_reply_dialog.dialog( "open" );
			    		$('#admin_request_reply_date').text(data.date);
			    		$('#admin_request_reply_category').text(data.category);
			    		$('#admin_request_reply_content').html(data.content);
			    		$('#admin_request_reply_depth').text(data.depth);
			    		$('#admin_request_reply_id').text(data.id);
			    	}
			    },
			    error : function(results){
		            alert(results.message);
			    }   
	        })
	      
	    });
	    
	    
	    //admin request replied
	    $( ".admin_request_Replied" ).button().on( "click", function() {
	    	
	    	var post_thread = $(this).attr("data");
			var dataString = 'post_thread='+ post_thread;
			
	        $.ajax({
	            type        : "POST",
	            url         : "/admin/View_getList",
	            data        : dataString,  
	            dataType    : "json",
	            encode      : true,

			    success : function(data){
			    	
			    	if(data.status == "success"){
			    		
			    		admin_request_replied_dialog.dialog( "open" );
			    		
			    		$('#request_date').html(data.date);
			    		$('#request_category').html(data.category);
			    		$('#request_content').html(data.content);
			    		

			    		$('#request_replied_content').html(data.replied_content);

			    		
			    		$('#request_replied_thread').html(data.thread);
			    		$('#request_replied_id').html(data.replied_id);
			    		
			    	}

			    },
			    error : function(results){
		            alert(results.message);
			    }   
	        })

	      
	    });

	    
		//User_replied
	    $( ".request_reply" ).button().on( "click", function() {

			//var post_thread = $("#post_thread").val();
			//var post_thread = $(this).parent().parent().attr("id");
			var post_thread = $(this).attr("data");
			var dataString = 'post_thread='+ post_thread;
			
	        $.ajax({
	            type        : "POST",
	            url         : "/mystate/ReplyPopup",
	            data        : dataString,  
	            dataType    : "json",
	            encode      : true,

			    success : function(data){
			    	
			    	if(data.status == "success"){
			    		
			    		user_reply_dialog.dialog( "open" );
						
			    		$('#reply_date').html(data.date);
			    		$('#reply_category').html(data.category);
			    		$('#reply_contents').html(data.content);
			    		$('#replied_contents').html(data.replied_content);
			    		
			    	}

			    },
			    error : function(results){
		            alert(results.message);
			    }   
	        })
	      		        
	    });
	 
	    
	    
	//Change_pw Ajax
	$(document).ready(function() {
	    // process the form
	    
	    $('#pw_form').submit(function(event) {
	
	        var oldpw = $("#oldpw").val();
			var newpw1 = $("#newpw1").val();
			var newpw2 = $("#newpw2").val();
			var dataString = 'oldpw='+ oldpw + '&newpw1='+ newpw1 + '&newpw2='+ newpw2;

	        $.ajax({
	            type        : "POST",
	            url         : "/Mystate/ChangePw",
	            data        : dataString,  
	            dataType    : "json",
	            encode      : true,

			    success : function(results){
			    	alert(results.message);
			    	if(results.status == "success"){
			    		dialog.dialog("close");
			    		window.location.reload();
			    	} else {
			    		
			    	}
			    },
			    error : function(results){
		            alert(results.message);
			    }   
	        })

	      event.preventDefault();
	   
	    });
		
	});
	

	//Menu
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


});

