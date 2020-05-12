---
order: 84
title: (LINUX) PHPmailer
category: Linux
---

해당 웹 사이트의 메일이 발송되는 곳에 class.smtp.php와 class.phpmailer.php만 FTP프로그램을 통하여 업로드하고
아래의 소스를 메일 발송될 페이지에 추가 시켜 줍니다.
 
$smtp_mail_id = "구글 메일이나 네이버메일 계정"; 예)test@naver.com 혹은 test@gmail.com 등의 형식
$smtp_mail_pw = "구글이나 네이버 ID의 패스워드"; 
$to_email = "받는사람메일주소"; 예) test@naver.com
$to_name = "받는사람 이름"; 예)홍길동
$title = "TEST 메일 제목"; 예)홍길동님의 문의사항 등록되었습니다. 
$from_name = "보내는사람 이름";
$from_email = "보내는사람 이메일";
$content = "메일내용 <br> html도 가능";
 
$smtp_use = 'smtp.naver.com'; //네이버 메일 사용시
//$smtp_use = 'smtp.gmail.com'; //구글 메일 사용시 주석제거
if ($smtp_use == 'smtp.naver.com') { 
$from_email = $smtp_mail_id; //네이버메일은 보내는 id로만 전송이가능함
}else {
 $from_email = $from_email; 
}
 
//메일러 로딩
require_once("class.phpmailer.php");
   
$mail = new PHPMailer(true);
$mail->IsSMTP();
try {
  $mail->Host = $smtp_use;   // email 보낼때 사용할 서버를 지정
  $mail->SMTPAuth = true;          // SMTP 인증을 사용함
  $mail->Port = 465;            // email 보낼때 사용할 포트를 지정
  $mail->SMTPSecure = "ssl";        // SSL을 사용함
  $mail->Username   = $smtp_mail_id; // 계정
  $mail->Password   = $smtp_mail_pw; // 패스워드
  $mail->SetFrom($from_email, $from_name); // 보내는 사람 email 주소와 표시될 이름 (표시될 이름은 생략가능)
  $mail->AddAddress($to_email, $to_name);  // 받을 사람 email 주소와 표시될 이름 (표시될 이름은 생략가능)
  $mail->Subject = $title;         // 메일 제목
  $mail->MsgHTML($content);         // 메일 내용 (HTML 형식도 되고 그냥 일반 텍스트도 사용 가능함)
  $mail->Send();              // 실제로 메일을 보냄
echo "메일을 전송하였습니다.";
 
} catch (phpmailerException $e) {
  echo $e->errorMessage();
} catch (Exception $e) {
   echo $e->getMessage();
}
주석에 적혀져 있는 내용을 꼼꼼히 보시고 자신에게 맞게 수정합니다.
 
이러면 네이버나 구글 등 포털 사이트의 SMTP를 이용해서 메일발송이 가능합니다.
홈페이지를 통하여 문의사항을 많이 받으시는 분이라면 화이트 도메인 문제로 인하여
난감한 상황에 빠졌을 때 SMTP를 사용하여 쉽게 해결하기 바랍니다.
