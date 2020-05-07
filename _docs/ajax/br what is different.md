---
order: 2
title: (Ajax) br what is different
category: Ajax
---

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

