---
order: 8
title: (PHP-codeig) [captcha]
category: Php - codeignitor
---

//controller
//		$url = base_url();
//		$captcha_word = rand(23678190, 96523469);
//		
//		$captcha = array(
//			'word'   => $captcha_word,
//			'img_path'  => './captcha/',
//			'img_url'  => ''.base_url().'captcha/',			
//			'img_width'  => '300',
//			'img_height'  => '50',
//			'expiration'  => '3600'
//			 
//		);
//		
//		$data['captcha'] = create_captcha($captcha);		 
//		print_r($data);	
		$this->load->view("request_view");
		
		
		
//view
<?=$captcha['image']?>

Chmod 777 capcha
