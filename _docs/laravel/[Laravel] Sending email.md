---
 order: 1
 title: ([Laravel) Sending email
 category: Laravel
 ---

 <br>
 1. server<br><br>
 php artisan make:controller ContactController<br>
 <br>
 2. vi /home/crypto/htdocs/portfolio/.env<br>
 MAIL_DRIVER=smtp<br>
 MAIL_HOST=smtp.gmail.com<br>
 MAIL_PORT=587<br>
 MAIL_USERNAME=emailaddress@gmail.com<br>
 MAIL_PASSWORD=passward<br>
 MAIL_ENCRYPTION=tls<br>
 <br>
 3. setting firewall<br>
 firewall-cmd --permanent --zone=public --add-port=587/tcp<br>
 systemctl restart firewalld.service<br>
 firewall-cmd --list-ports<br>
 <br>
 4. google account<br>
 Turn on<br>
 account -> security -> Less secure app access<br>
 <br>
 5. contact form(writing form)<br>
 contact.blade.php<br>
 <br>
 <form action="contact" method="post" role="form" class="php-email-form"><br>
     {{@csrf_field()}}<br>
       <div class="form-row"><br>
 	<div class="col-md-6 form-group"><br>
 	  <input type="text" name="name" class="form-control" id="name" placeholder="Your Name" data-rule="minlen:4" data-msg="Please enter at least 4 chars" /><br>
 	  <div class="validate"></div><br>
 	</div><br>
 	<div class="col-md-6 form-group"><br>
 	  <input type="email" class="form-control" name="email" id="email" placeholder="Your Email" data-rule="email" data-msg="Please enter a valid email" /><br>
 	  <div class="validate"></div><br>
 	</div><br>
       </div><br>
       <div class="form-group"><br>
 	<input type="text" class="form-control" name="subject" id="subject" placeholder="Subject" data-rule="minlen:4" data-msg="Please enter at least 8 chars of subject" /><br>
 	<div class="validate"></div><br>
       </div><br>
       <div class="form-group"><br>
 	<textarea class="form-control" name="message" rows="6" data-rule="required" data-msg="Please write something for us" placeholder="Message"></textarea><br>
 	<div class="validate"></div><br>
       </div><br>
       <div class="mb-3"><br>
 	<div class="loading">Loading</div><br>
 	<div class="error-message">Unfortunately failing sending e-mail.</div><br>
 	<div class="sent-message">Your message has been sent. Thank you!</div><br>
       </div><br>
       <div class="text-center"><button type="submit">Send Message</button></div><br>
     </form><br>
 <br>
 6. set up route.php<br>
 Route::post('contact', 'ContactController@send');<br>
 <br>
 7. ContactController.php<br>
 add below<br>
 use Redirect,Response,DB,Config;<br>
 use Mail;<br>
 <br>
 code<br>
 public function send(Request $req){<br>
         <br>
         $name = $req->input('name');<br>
         $email = $req->input('email');<br>
         $subject = $req->input('subject');<br>
         $text = $req->input('message');<br>
         $title = 'Aaron Portfolio Mail';<br>
        <br>
         $data['name'] = $name;<br>
         $data['email'] = $email;<br>
         $data['subject'] = $subject;<br>
         $data['text'] = $text;<br>
         $data['title'] = $title;<br>
         <br>
         Mail::send('emails.email', $data, function($message) {<br>
             $message->to('jfluke1414@gmail.com', 'Aaron(Hyunjin Yeo)')->subject('From Aaron Portfolio page');<br>
         });<br>
                 <br>
         if (Mail::failures()) {<br>
 //             return response()->Fail('Sorry! Please try again.');<br>
             echo "Failed";<br>
         } else {<br>
 //             return response()->success('Great! Successfully sended this E-mail to Aaron');<br>
             echo "Sent";<br>
         }<br>
                     <br>
     }<br>
 <br>
 8. make viewfile for email form(e-mail will be sent by a form below)<br>
 at view/emails/email<br>
 <br>
 email.php<br>
 <!DOCTYPE html><br>
 <html lang="en"><br>
 <br>
     <head><br>
       <meta charset="utf-8"><br>
       <meta content="width=device-width, initial-scale=1.0" name="viewport"><br>
     <br>
       <title>{{ $title }}</title><br>
 <br>
     </head><br>
         <body><br>
         	<p1>{{ $name }}</p1><br>
         	<p>{{ $email }}</p><br>
         	<p>{{ $subject }}</p><br>
         	<p>{{ $text }}</p><br>
         	<br>
         	<p1>This is from Aaron's portfolio server from someeles</p1><br>
     	</body><br>
 <br>
 </html><br>
 