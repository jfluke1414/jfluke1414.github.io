---
order: 2
title: (Library) [MCRYPT] 압축 라이브러리 
category: Library
---

암호화에 대한 기본 상식
암호화(Encryption)의 방식에는 단방향 암호화, 대칭 암호화, 비대칭 암호화가 있다.
단방향 암호화(One-way Encryption)는 복호화할 수 없도록 하는 방식이다. 이 방식에서는 해시 알고리즘(Hash Algorithm)을 사용하는데, 이 과정을 통해 고유한 지문(Fingerprint)을 생성한다.
일반적으로, 단방향 암호화를 통해 얻은 값으로는 복호화가 불가능하다고 하는데 원문이 짧거나 일반적으로 널리 사용되는 문자열일 경우에는 무작위 값 입력을 통한 공격(Brute Force Attack)을 통해 무력화되기 쉽다.
MD5, SHA1 등이 대표적인 해시 알고리즘이다.
대칭 암호화(Symmetric Encryption)는 키(Key)를 통해 동일한 알고리즘으로 암호화/복호화를 하는 방법이다. 이 방식은 2차 세계대전 중에 암호화 기계(Enigma Machine)에 사용된 방식이다.
암호화/복호화에 필요한 키가 유출되지만 않는다면 매우 안전한 방식이다. DES, TWOFISH, GOST 등이 대표적인 알고리즘이다.
비대칭 암호화(Asymmetric Encryption)는 SSL 같은 방식이라고 하는데, 자세한 내용은 모르므로 넘어가겠다.
이 글에서는 PHP에서 대칭 암호화 방식을 통한 암호화/복호화에 대해 설명하겠다.
Mcrypt 라이브러리의 설치와 설정
PHP에서는 Mcrypt 라이브러리를 통해 대칭 암호화를 지원한다. 따라서 Mcrypt를 이용하려면 라이브러리를 추가로 설치해 주어야 한다.
http://mcrypt.sourceforge.net/에서 Mcrypt 라이브러리를 다운로드 받을 수 있으며, 윈도우 서버라면 http://files.edin.dk/php/win32/mcrypt/에서 컴파일된 라이브러리 파일을 다운로드 받아 사용할 수 있다. 작동하도록 설정하려면 php.ini의 설정을 변경해 주어야 하는데, 자세한 설정 방법은http://www.php.net/manual/kr/book.mcrypt.php 에서 확인할 수 있다.
데비안 계열 리눅스 서버라면 터미널에서 다음의 명령어를 입력하는 것으로 Mcrypt를 설치와 설정을 완료할 수 있다.
view source
print?
1.$ sudo apt-get install php5-mcrypt
2.$ sudo apt-get install libmcrypt4
3.$ sudo /etc/init.d/apache2 restart
Mcrypt를 이용한 암호화/복호화 예제
다음의 코드를 보면 쉽게 이해할 수 있다.
view source
print?
01.$key = "열쇠";
02.$plainData = "개인정보";
03.$encryptedDataOnBinary = mcrypt_ecb(MCRYPT_GOST, $key, $plainData, MCRYPT_ENCRYPT);
04.$encryptedData = base64_encode($encryptedDataOnBinary);
05.echo "암호화 할 평문 : ".$plainData;
06.echo "<BR>
07.";
08.echo "암호화 결과로 나온 바이너리 값: ".$encryptedDataOnBinary;
09.echo "<BR>
10.";
11.echo "암호화 결과를 아스키 코드로 변환한 값 : ".$encryptedData;
앞서 설명했듯, 대칭 암호화를 하기 위해서는 키가 필요하다. 이 예제에서는 $key로 "열쇠"라는 임의의 문자열을 넣었는데 실제로는 더 복잡하고 고유한 것을 사용하는 것이 좋겠다. $plainData는 암호화 할 대상을 말한다. 이 예제에서는 예로 "개인정보"라는 문자열을 넣어보았다.
mcrypt는 여러 기본 함수를 제공하는데, 그 중 이번에는 mcrypt_ecb() 함수를 이용했다. 참고로 ECB란 전자 부호표 모드(Electric CodeBook mode)의 약자다. mcrypt_ecb() 함수에는 네 가지 값을 넣어주어야 하는데, Mcrypt에서 제공하는 알고리즘 상수, 키, 암호화 할 값, 암호화/복호화를 위한 상수가 그것이다.
Mcrypt에서는 DES, TWOFISH, GOST 등 많은 알고리즘을 지원하는데 이 목록은http://www.php.net/manual/en/mcrypt.ciphers.php에서 확인할 수 있다. 이 예제에서는 GOST 방식을 사용하기 위해 MCRYPT_GOST라는 상수를 사용했다. 또한 이 예제에서는 암호화을 할 것이므로 MCRYPT_ENCRYPT라는 상수도 넣었다.
이렇게 Mcrypt를 통해 암호화를 하면 그 결과로 바이너리(Binary) 값을 반환한다. 즉, 컴퓨터만 이해할 수 있는 2진수 데이터를 반환한다는 의미다. 따라서 브라우저는 "'ӫ {3 ѠO# c ʾfBg "와 같이 인간도, 브라우저도 이해할 수 없는 결과를 출력할 것이다.
이 문제는 base64_encode() 함수를 이용함으로써 해결할 수 있다. 결과적으로 "8UHT/jWsIopHDCUpbfJLIA=="와 같이 아스키 코드로 변환한 값을 얻을 수 있다. 이로써 암호화가 성공적으로 이루어졌다.
이제 복호화 코드를 보자.
view source
print?
1.$decryptedDataOnBinary = base64_decode($encryptedData);
2.$decryptedData = mcrypt_ecb(MCRYPT_GOST, $key, $decryptedDataOnBinary, MCRYPT_DECRYPT);
3.echo "바이너리 값으로 다시 변환한 암호화 결과 값 : ".$decryptedDataOnBinary;
4.echo "<BR>
5.";
6.echo "바이너리 값을 복호화 한 결과 값 : ".$decryptedData;
앞서 (아스키 코드로 까지) 암호화한 결과 값을 base64_decode() 함수를 이용해 다시 바이너리 값으로 변환한다. 이 값을 다시 mcrypt_ecb() 함수를 이용해 복호화 하기 위해, 앞서 암호화하기 위해 사용했던 알고리즘의 상수인 MCRYPT_GOST, 앞서 암호화 하기 위해 사용했던 키, 바이너리로 다시 변환한 암호화 결과 값, 복호화를 위한 상수 MCRYPT_DECRYPT를 넣는다. 그 결과로 복호화 된 결과 값인 $decryptedData를 출력하면 "개인정보"라는 문자열을 얻게 된다. 이로써 복호화도 성공적으로 이루어졌다.
위의 결과를 아래와 같이 함수로 정리하면 편리하게 사용할 수 있다.
view source
print?
01.// mcrypt.php
02.$key = "1dasd12WESA12dsaasd456TGDFsd";
03.
04./**
05.* 데이터 암호화 함수
06.*/
07.function function_for_encryption($plain_data){
08. 
	global $key;
09. 
	$encrypted_data_on_binary = mcrypt_ecb (MCRYPT_SERPENT, $key, $plain_data, MCRYPT_ENCRYPT);
10. 
	$encrypted_data = base64_encode($encrypted_data_on_binary);
11. 
	return $encrypted_data;
12.}
13.
14./**
15.* 데이터 복호화 함수
16.*/
17.function function_for_decryption($encrypted_data){
18. 
	global $key;
19. 
	$decrypted_data_on_binary = base64_decode($encrypted_data);
20. 
	$plain_data = mcrypt_ecb (MCRYPT_SERPENT, $key, $decrypted_data_on_binary, MCRYPT_DECRYPT);
21. 
	return $plain_data;
22.}
Mcrypt를 이용한 암호화/복호화를 DB 입력/조회에 적용하기
이제 암호화/복호화를 DB 입력/조회에 적용해 보겠다.
DB에는 mailing_list라는 테이블이 있고 그 안에 no, name, email, date라는 필드가 있고 no 필드는 int이며 Auto Increment, 나머지 필드는 모두 varchar라고 가정한다.
POST 값으로 다음과 같은 메일링리스트 가입 정보를 받았다고 가정하자.
view source
print?
1.Array (
2. 
	[name] => testman
3. 
	[email] => test@example .com
4. 
	[date] => 20110521
5.)
이제 POST로 넘겨받은 모든 값을 암호화 해서 DB에 입력할 것이다.
view source
print?
01.// insertDB.php
02.include ./dbConnect.php; // DB 연결 (구체적인 코드는 생략한다)
03.include ./mcrypt.php;
04.
05.foreach($_POST as $key => $value) {
06. 
	$_POST[$key] = function_for_encryption($value);
07.}
08.$query = "INSERT INTO `mailing_list` (`name`, `email`, `date`)
09. 
	VALUES ('{$_POST['name']}', '{$_POST['email']}','{$_POST['date']}')";
10.$result = mysql_query($query);
이제 mailing_list 테이블의 모든 데이터를 조회해서 복호화 한 다음, 화면에 출력할 것이다.
view source
print?
01.//selectDB.php
02.include ./dbConnect.php; //DB 연결 (구체적인 코드는 생략한다)
03.include ./mcrypt.php;
04.
05.$query = "SELECT * `mailing_list`";
06.$result = mysql_query($query);
07.$number_of_rows = mysql_num_rows($result);
08.for ($i=0; $i<$number_of_rows; $i++){
09. 
	$row = mysql_fetch_array($result);
10. 
	foreach($row as $key => $value) {
11. 
	if ($key=='no') {
12. 
		continue; // $row['no']는 복호화 할 필요가 없다.
13. 
	}
14. 
	$row[$key] = function_for_decryption($value);
15. 
	}
16. 
	echo "번호 : ".$row['no']." 이름 : ".$row['name']." 이메일 : ".$row['email']." 날짜".$row['date'];
17.}
