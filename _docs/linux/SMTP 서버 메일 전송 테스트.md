---   
order: 83   
title: (LINUX) SMTP 서버 메일 전송 테스트   
category: Linux   
---   
   
[발신]   
   
telnet localhost 25   
helo localhost   
mail from : scbyun@mail.vm.scbyun.com   
rcpt to : scbyun@mail.vm.scbyun.com   
data   
subject : Test Mail   
테스트 메일 입니다.   
테스트 메일 입니다.   
테스트 메일 입니다.   
테스트 메일 입니다.   
테스트 메일 입니다.   
.   
quit   
    
   
# telnet localhost 25 <=   
Trying ::1...   
telnet: connect to address ::1: Connection refused   
Trying 127.0.0.1...   
Connected to localhost.   
Escape character is '^]'.   
220 e_vm03 ESMTP Sendmail 8.14.4/8.14.4; Wed, 6 Aug 2014 18:02:49 +0900   
helo localhost   
250 e_vm03 Hello localhost [127.0.0.1], pleased to meet you   
mail from : scbyun@mail.vm.scbyun.com <= 보내는 사람 주소   
250 2.1.0 scbyun@mail.vm.scbyun.com... Sender ok   
rcpt to : scbyun@mail.vm.scbyun.com <= 받는 사람 주소   
250 2.1.5 scbyun@mail.vm.scbyun.com... Recipient ok   
data   
354 Enter mail, end with "." on a line by itself   
subject : Test Mail   
테스트 메일 입니다.   
테스트 메일 입니다.   
테스트 메일 입니다.   
테스트 메일 입니다.   
테스트 메일 입니다.   
.   
250 2.0.0 s7692nLf005822 Message accepted for delivery   
quit   
221 2.0.0 e_vm03 closing connection   
Connection closed by foreign host.   
#   
    
[수신]   
   
Part 3.3:   
Content-Type: message/rfc822   
    
From scbyun@mail.vm.scbyun.com Wed Aug  6 18:02:58 2014   
Return-Path: <scbyun@mail.vm.scbyun.com>   
Date: Wed, 6 Aug 2014 18:02:49 +0900   
From: scbyun@mail.vm.scbyun.com   
subject: Test Mail   
    
테스트 메일 입니다.   
테스트 메일 입니다.   
테스트 메일 입니다.   
테스트 메일 입니다.   
테스트 메일 입니다.   
&   
    
