---
order: 6
title: (PHP-codeig) function upload_file()
category: Php - codeignitor
---

function upload_file()
	{
		
		$config['upload_path'] = './manual';
		$config['allowed_types'] = 'gif|jpg|jpeg|png|iso|dmg|zip|rar|doc|docx|xls|xlsx|ppt|pptx|csv|ods|odt|odp|pdf|rtf|sxc|sxi|txt|exe|avi|mpeg|mp3|mp4|3gp';
		$config['max_size']	= '1024';
		$config['max_width']  = '1024';
		$config['max_height']  = '768';
	
		$this->load->library('upload', $config);
		
		if ( ! $this->upload->do_upload("upload_file"))
		{
			$error = array('error' => $this->upload->display_errors());
			$msg = $error;
			echo("<script>alert('$msg');history.back();</script>");
			echo("<script>JavaScript:window.close();</script>");
		}
		else
		{
			$upload_data = $this->upload->data();

			$this->load->model('Administrator');
			$this->Administrator->save_uploadInfo($upload_data);
			
			$msg = "업로드 완료하였습니다.";
			echo("<script>alert('$msg');history.back();</script>");
			echo("<script>JavaScript:window.close();window.opener.top.location.reload()</script>");
			
		}
	}

