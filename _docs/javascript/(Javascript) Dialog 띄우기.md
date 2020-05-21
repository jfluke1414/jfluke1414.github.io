---   
order: 14   
title: (Javascript) Dialog 띄우기    
category: Javascript   
---   
   
```   
	1. <span id="admin_edit_save"><img src="/assets/img/bt_save.gif" width="96" height="42" alt=""/></span>   
	2. //admin_edit_save   
	    $( "#admin_edit_save" ).button().on( "click", function() {   
	    	   
	    	id = $("#admin_edit_id").text();   
	    	content = $("#edit_replied_content").val();   
			//replace(/\r   \n|   \n|\r/g, '<br />');   
			var dataString = 'post_id='+ id + '&post_content='+ content;   
			   
	        $.ajax({   
	            type        : "POST",   
	            url         : "/admin/edit_update",   
	            data        : dataString,     
	            dataType    : "json",   
	            encode      : true,   
   
			    success : function(data){   
			    	   
			    	if(data.status == "success"){   
			    		alert(data.message);   
			    		admin_popup_edit_dialog.dialog( "open" ); // dialog open   
			    		admin_popup_edit_dialog.dialog( "close" ); // dialog close   
			    		admin_request_replied_dialog.dialog( "close" );   
						데이터 표출   
						$('#admin_doc_change_filename').text(data.filename);   
						$('#select_change_filename').val(data.filename);   
			   
						윈도우 리로드   
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
   
	Dialog 만들기   
	3. admin_popup_edit_dialog = $( "#admin_popup_edit_dialog" ).dialog({   
		      autoOpen: false,   
		      height: 550,   
		      width: 550,   
		      modal: true,   
		      resizable: false,   
			  draggable: true,   
			     
		    });   
```