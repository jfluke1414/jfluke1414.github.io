---
order: 5
title: Ajax 값 전송 Html로 표출
category: Php
---

$('#request_replied_content').html(data.replied_content);


 //admin request replied
	    $( ".admin_request_Replied" ).button().on( "click", function() {
	    	
	    	var post_thread = $(this).attr("data");
			var dataString = 'post_thread='+ post_thread;
//	    	var post_thread = $("#post_thread").val();
//			var dataString = 'post_thread='+ post_thread;
			
//			alert(dataString);
	        $.ajax({
	            type        : "POST",
	            url         : "/admin/View_getList",
	            data        : dataString,  
	            dataType    : "json",
	            encode      : true,

			    success : function(data){
			    	
			    	if(data.status == "success"){
			    		
			    		admin_request_replied_dialog.dialog( "open" );
//			    		$('#user_reply_dialog').text(results);

						
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