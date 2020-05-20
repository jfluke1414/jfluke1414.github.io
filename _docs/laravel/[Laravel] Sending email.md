---   
 order: 1   
 title: (Laravel) Sending email   
 category: Laravel   
---   
   
*### server   
 php artisan make:controller ContactController   
    
*### vi /home/crypto/htdocs/portfolio/.env   
 MAIL_DRIVER=smtp   
 MAIL_HOST=smtp.gmail.com   
 MAIL_PORT=587   
 MAIL_USERNAME=emailaddress@gmail.com   
 MAIL_PASSWORD=passward   
 MAIL_ENCRYPTION=tls   
    
*### setting firewall   
 firewall-cmd --permanent --zone=public --add-port=587/tcp   
 systemctl restart firewalld.service   
 firewall-cmd --list-ports   
    
*### google account   
 Turn on   
 account -> security -> Less secure app access   
    
*### contact form(writing form)   
 contact.blade.php   
'''   
 <form action="contact" method="post" role="form" class="php-email-form">   
     {{@csrf_field()}}   
       <div class="form-row">   
 	<div class="col-md-6 form-group">   
 	  <input type="text" name="name" class="form-control" id="name" placeholder="Your Name" data-rule="minlen:4" data-msg="Please enter at least 4 chars" />   
 	  <div class="validate"></div>   
 	</div>   
 	<div class="col-md-6 form-group">   
 	  <input type="email" class="form-control" name="email" id="email" placeholder="Your Email" data-rule="email" data-msg="Please enter a valid email" />   
 	  <div class="validate"></div>   
 	</div>   
       </div>   
       <div class="form-group">   
 	<input type="text" class="form-control" name="subject" id="subject" placeholder="Subject" data-rule="minlen:4" data-msg="Please enter at least 8 chars of subject" />   
 	<div class="validate"></div>   
       </div>   
       <div class="form-group">   
 	<textarea class="form-control" name="message" rows="6" data-rule="required" data-msg="Please write something for us" placeholder="Message"></textarea>   
 	<div class="validate"></div>   
       </div>   
       <div class="mb-3">   
 	<div class="loading">Loading</div>   
 	<div class="error-message">Unfortunately failing sending e-mail.</div>   
 	<div class="sent-message">Your message has been sent. Thank you!</div>   
       </div>   
       <div class="text-center"><button type="submit">Send Message</button></div>   
     </form>   
'''    
*### set up route.php   
 Route::post('contact', 'ContactController@send');   
    
*### ContactController.php   
 add below   
 use Redirect,Response,DB,Config;   
 use Mail;   
    
<pre>
<code>
 public function send(Request $req){   
            
    $name = $req->input('name');   
    $email = $req->input('email');   
    $subject = $req->input('subject');   
    $text = $req->input('message');   
    $title = 'Aaron Portfolio Mail';   
     
    $data['name'] = $name;   
    $data['email'] = $email;   
    $data['subject'] = $subject;   
    $data['text'] = $text;   
    $data['title'] = $title;   
       
    Mail::send('emails.email', $data, function($message) {   
        $message->to('jfluke1414@gmail.com', 'Aaron(Hyunjin Yeo)')->subject('From Aaron Portfolio page');   
    });   
               
    if (Mail::failures()) {   
//             return response()->Fail('Sorry! Please try again.');   
        echo "Failed";   
    } else {   
//             return response()->success('Great! Successfully sended this E-mail to Aaron');   
        echo "Sent";   
    }   
                   
}   
</pre>
</code>   

*### make viewfile for email form(e-mail will be sent by a form below)   
 at view/emails/email   
    
 email.php   
 '''
 <!DOCTYPE html>   
 <html lang="en">   
    
    <head>   
      <meta charset="utf-8">   
      <meta content="width=device-width, initial-scale=1.0" name="viewport">   
       
      <title>{{ $title }}</title>   
   
    </head>   
        <body>   
        <p1>{{ $name }}</p1>   
        <p>{{ $email }}</p>   
        <p>{{ $subject }}</p>   
        <p>{{ $text }}</p>   
           
        <p1>This is from Aaron's portfolio server from someone eles</p1>   
    </body>   
    
 </html>   
 '''