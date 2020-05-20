---
title: (API) Facebook API
category: Api
order: 1
---

### 1. 새 애플리케이션 만들기
### 2. 인증과 토큰 생성
### 3. 웹 브라우저 조회하기(URL 이용)
### 4. JSON 리턴 값 확인

- 앱 ID
136194889764191
- API 키
5061a112083e3a3537ffe3f4e5e7ec2c
- 앱 시크릿 코드
bbdb36dc273dca291bd4d33a602067bc

-- Access Token Key
access_token=136194889764191|2.2_xUFhalO0lNZs2V6AXUjQ__.3600.1305162000.1-100001739791527|i5jHVEhBCYGEID9Ixdm5kgUZ_HE&expires=4272

로그인 되었을때 가능함.

-- Access code 얻는 방법 
https://www.facebook.com/dialog/oauth?client_id=[앱 ID]&redirect_uri=http://www.facebook.com/connect/login_success.html

-- Access Code
http://www.facebook.com/connect/login_success.html?code=Oi0ylFRuhsVloBNNzE1LB2PGKtRo8aB0iJ5IC6UYGaA.eyJpdiI6IjZNZXhEZ3NaQmlucVYtckp3dnEyYXcifQ.NorQtmnPNaxbKM176Zq7lo_xu7F5QPtmL9lf1aC4DigkwVtgTEBWk9GG_mtgvqMc0OcoZAaVPo9ZFHO5Vtb6iUGvRkdy7B-8tx7o7TtI6kT6r0AgchbgZ0ydPSMEuMmqmTF6eClizcTn1AELLzB3IA

-- Access Token 얻는 방법
https://graph.facebook.com/oauth/access_token?client_id=[앱 ID]&redirect_uri=http://www.facebook.com/connect/login_success.html&client_secret=[시크릿 code]&code=Oi0ylFRuhsVloBNNzE1LB2PGKtRo8aB0iJ5IC6UYGaA.eyJpdiI6IjZNZXhEZ3NaQmlucVYtckp3dnEyYXcifQ.NorQtmnPNaxbKM176Zq7lo_xu7F5QPtmL9lf1aC4DigkwVtgTEBWk9GG_mtgvqMc0OcoZAaVPo9ZFHO5Vtb6iUGvRkdy7B-8tx7o7TtI6kT6r0AgchbgZ0ydPSMEuMmqmTF6eClizcTn1AELLzB3IA

-- Access Token
https://graph.facebook.com/oauth/access_token?client_id=136194889764191&redirect_uri=http://www.facebook.com/connect/login_success.html&client_secret=04edde2d60835092a8d137ca4decd8b6&code=RueJiAcW_Ir4CFZMr6sOiPNCM_gNWB3Uft84ad85nLE.eyJpdiI6IjBfa1ZxWHBCZjBuTEVDZF9Rd3M3RncifQ.rEKDKJ-oOIGip9eZdp7D62qO7Hp7mkN91uSSc48P5rEo8gNe9qIr0r3qXO0bvbHsmbcBE588pvF8JnC9gAQJ7_ttybNcCVEuSUcLaAPXzG-X6iErsDtv5c5KVuA0iNN9UC9OFkl


access_token=136194889764191|2.QNaXiDxVt_Y8XI2IezmiHQ__.3600.1305129600.1-100001739791527|zkNYgRhetFb-O0MsXfyf9zAUGRo&expires=4286


사용 URL : https://graph.facebook.com/[Object ID]/[연결 사항]?access_token=[access_token]

- 개인 정보 가져오기
https://graph.facebook.com/me?access_token=136194889764191|2.QNaXiDxVt_Y8XI2IezmiHQ__.3600.1305129600.1-100001739791527|zkNYgRhetFb-O0MsXfyf9zAUGRo&expires=4286
예)
https://graph.facebook.com/[친구의 user id]?access_token=136194889764191|2.QNaXiDxVt_Y8XI2IezmiHQ__.3600.1305129600.1-100001739791527|zkNYgRhetFb-O0MsXfyf9zAUGRo&expires=4286
-- 친구 목록 가져오기
https://graph.facebook.com/me/friends?access_token=136194889764191|2.QNaXiDxVt_Y8XI2IezmiHQ__.3600.1305129600.1-100001739791527|zkNYgRhetFb-O0MsXfyf9zAUGRo&expires=4286
예)
https://graph.facebook.com/[친구의 user id]?access_token=136194889764191|2.QNaXiDxVt_Y8XI2IezmiHQ__.3600.1305129600.1-100001739791527|zkNYgRhetFb-O0MsXfyf9zAUGRo&expires=4286
-- LIKES 가져오기
https://graph.facebook.com/me/likes?access_token=136194889764191|2.QNaXiDxVt_Y8XI2IezmiHQ__.3600.1305129600.1-100001739791527|zkNYgRhetFb-O0MsXfyf9zAUGRo&expires=4286
예)

https://graph.facebook.com/[친구의 user id]/likes?access_token=136194889764191|2.QNaXiDxVt_Y8XI2IezmiHQ__.3600.1305129600.1-100001739791527|zkNYgRhetFb-O0MsXfyf9zAUGRo&expires=4286