---   
order: 18   
title: (Javascript) Pattern check 정규표현식 유효성 검사   
category: Javascript   
---   
   
```   
//<![CDATA[   
/*   
 var txt="abc 123";   
 var reExp=/^\D+\s+\d+/ig;   
 //var chk1=reExp.test(txt);   
 //console.log(chk1);   
 var chk2=reExp.exec(txt);   
 console.log(chk2);   
*/   
/*   
 var txt="123";   
 var reExp=/^\D*\s+\d+/ig;   
 //var chk1=reExp.test(txt);   
 //console.log(chk1);   
 var chk2=reExp.exec(txt);   
 console.log(chk2);   
*/   
/*   
 var txt="abc 123";   
 var reExp=/^(a|b|c)?\s+\d+/ig;   
 //var chk1=reExp.test(txt);   
 //console.log(chk1);   
 var chk2=reExp.exec(txt);   
 console.log(chk2);   
*/   
/*   
 var txt="abc 123";   
 var reExp=/123$/ig; //$문장끝이 123으로 끝나는지?   
 //var chk1=reExp.test(txt);   
 //console.log(chk1);   
 var chk2=reExp.exec(txt);   
 console.log(chk2);   
*/   
/*   
 var txt="abc 123";   
 var reExp=/^[a-z]+\s+123$/ig; //a-z까지 시작해서. 끝($)은 123으로끝나게   
 //var chk1=reExp.test(txt);   
 //console.log(chk1);   
 var chk2=reExp.exec(txt);   
 console.log(chk2);   
*/   
/*   
 var txt="abc 123";   
 var reExp=/^[a-z]{1,3}+123$/ig; //a-z까지 3글자까지   
 //var chk1=reExp.test(txt);   
 //console.log(chk1);   
 var chk2=reExp.exec(txt);   
 console.log(chk2);   
*/   
/*   
 var txt="abc 123";   
 var reExp=/^[a-z]{3,}\s+123$/ig; //a-z까지 3글자이상 나와야 한다   
 //var chk1=reExp.test(txt);   
 //console.log(chk1);   
 var chk2=reExp.exec(txt);   
 console.log(chk2);   
*/   
/*   
 var txt="가나다 123";   
 var reExp=/^[가-힣]{3,}\s+123$/ig; //한글이 나와야 할때는 가에서 부터 힣까지   
 //var chk1=reExp.test(txt);   
 //console.log(chk1);   
 var chk2=reExp.exec(txt);   
 console.log(chk2);   
*/   
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ   
  //전화번호 유효성 검사    
  function phoneChk(){   
   var myNum = document.getElementById("phoneNumber").value;   
   var rgEx = /[01](0|1|6|7|8|9)[-](\d{4}|\d{3})[-]\d{4}$/g;   
   var OK = rgEx.test(myNum);   
   if(!OK){   
    alert("잘못입력하셨습니다.");   
    return false;   
   }   
   else{   
    alert("정상입력하였습니다.");   
   }   
  }   
 //]]>   
</script>   
</head>   
    
<body>   
 <form name="form1" method="post" action="" onsubmit="return phoneChk();">   
  <label for="phoneNumber">TEL</label><input type="text" name="phoneNumber" id="phoneNumber" />   
  <input type="submit" value="확인" />   
 </form>   
</body>   
</html>   
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ   
 window.onload        =function(){   
   document.form1.onsubmit = function(){   
   /*아이디   
   1. 영문시작 다음 영문,밑줄,숫자(5~12)   
    홈페이지*/   
     var myId = this.user_id.value;   
     var regExp2 = /^[a-z]{1}\w{4,11}/ig;   
     var chk2 = regExp2.test(myId);   
     if(!chk2){   
      alert("잘못된 아이디 형식입니다~!!!");   
      return false;   
     }   
   /*계정 @ 도메인주소   
     1. 계정시작은 영문, 밑줄, 숫자, 영문 5~12   
     2. "@"   
     3. 도메인 명 영문, 숫자, _ 2~20   
     4. "."   
     5. 영문 2~4 co.kr, .com, .net   
    6. . 영문 *  ? */   
      var myMail = this.email.value;   
      var regExp =/^[a-z].\w{5,12}@\w{2,20}[\.][a-z]{2,4}([\.][a-z]{2,3})?$/ig;   
      var chk = regExp.test(myMail);   
      //alert(chk);   
      if(!chk){   
       alert("잘못된 이메일 형식입니다~!!!");   
       return false;   
      }   
    /*   
   1. http:// 시작   
   2. 영문 3~12   
   3. "."   
   4. 영문    
   5. "."   
   6. 영문 "."   
   7. "."영문 : 와도되고 안와도되고 */   
     var mySite = this.mySite.value;   
     var regExp3 = /^(http\:\/\/){1}\w{3,12}[\.]\w{2,20}[\.][a-z]{2,4}([\.][a-z]{2,3})?$/ig;   
     var chk3 = regExp3.test(mySite);   
     if(!chk3){   
      alert("잘못된 url 형식입니다~!!!!");   
      return false;   
     }   
   /*전화번호   
   1. 지역번호    
   2. -    
   3. 국번 숫자 3~4   
   4. -    
   5. 번호 4개*/   
   var myTel = this.myTel.value;   
   var regExp4 = /[0](2|51|53|32|62|42|52|31)[-][0-9]{3,4}[-]{0-9}[4]/;   
   var chk4 = regExp4.test(myTel);   
   if(!chk4){   
    alert("잘못된 전화번호 형식입니다~!!!");   
    return false;   
   }   
    
   }   
  }   
 //]]>   
    
    
</script>   
</head>   
    
<body>   
 <!--<form name="form1" method="post" action="" onsubmit="return phoneChk();">   
  <label for="phoneNumber">TEL</label><input type="text" name="phoneNumber" id="phoneNumber" />   
  <input type="submit" value="확인" />-->   
 <form name="form1" method="post" action="http://www.naver.com">   
  <p>   
   <label for="user_id">아이디</label>   
   <input type="text" name="user_id" id="user_id"/>   
  </p>   
  <p>   
   <label for="email">이메일</label>   
   <input type="text" name="email" id="email"/>   
  </p>   
  <p>   
   <label for="mySite">홈페이지</label>   
   <input type="text" name="mySite" id="mySite"/>   
  </p>   
  <p>   
   <label for="myTel">전화번호</label>   
   <input type="text" name="myTel" id="myTel"/>   
  </p>   
  <p>   
   <input type="submit" value="전송" />   
  </p>   
 </form>   
</body>   
```