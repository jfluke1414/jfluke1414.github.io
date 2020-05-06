---
title: Twitter API & Oauth
category: Api
order: 2
---

마이크로 블로깅으로 큰 인기를 얻고 있는 트위터는 거의 모든기능을 OpenAPI로 제공하고 있고 최근엔 그나마 나아졌지만 트위터사이트에서는 별다른 UX적인 편리함을 주는 것이 없기 때문에 대부분의 유저들은 데스크탑 클라이언트 혹은 다른 웹사이트들을 이용해서 트위터를 더 많이 사용하고 있습니다. 이렇게 클라이언트를 만들려면 트위터에서 제공하는 OpenAPI를 이용해서 개발해야 하는데 Twitter는  API문서화가 꽤 잘 되어 있는 편인데다가 다행히도 각 언어별로 상당수의 트위터 라이브러리들이 제공되고 있기에 가져다가 편리하게 쓸 수 있습니다. 이번에 M31 프로젝트를 하면서 Java로 트위터 웹클라이언트를 만들어야 해서 라이브러리들을 둘러 보았지만 Twitter4J 를 선택했습니다.

 현재 Java 트위터 라이브러리 로는 Twitter4J , java-twitter , jtwitter , Twitter Client 
의 총 4가지를 존재하고 있습니다. 이 중에서 Twitter4J를 선택한 것은 문서화가 잘 되어 있고, 지속적으로 업데이트가 되고 있기 때문입니다. 


OAuth 사용하기
트위터의 외부에서의 인증을 위해서 OAuth 를 사용하고 있는데 OAuth사이트에서는 OAuth를 다음과 같이 정의하고 있습니다.

An open protocol to allow secure API authorization in a simple and standard method from desktop and web applications. (데스크탑과 웹어플리케이션에서 간단하고 표준적인 방법으로 안전한 API 인증을 하도록 하는 공개 프로토콜입니다.)
OAuth는 Identity 2.0으로 넘어오면서 OpenID와 함께 생겨난 대표적인 인증 표준이라고 할 수 있습니다.API에서 제공되는 것 내에서만 사용했기에 직접 구현한 것은 아니라서 사용했다고 하기는 뭐하지만 어쨌든 OAuth를 사용한 것은 이번이 처음이었습니다. OpenID에 대해서는 이전에 올렸던 글을 참고하시면 되겠습니다. 

인증메커니즘 자체도 약간 비슷한 느낌이긴 합니다만 OpenID는 OpenID Provider가 인증을 책임지고 Consumer에서는 아이디만 Provider측에 넘겨주면 Provider가 인증된 결과를 돌려주게 됩니다. Consumer는 인증에 대해서는 전혀 책임지지 않고 로그인인증을 Provider에 위임하게 됩니다. 반면에 OAuth는 좀더 진보된 인증방식이라고 할 수 있습니다.

어떤 기술을 이해하는데는 스펙을 보는 것이 가장 정확하고 좋기는 하지만 영어권이 아닌 저희로써는 영어문서는 울렁증이나서 오래보는것이 만만치 않고 또 개발하면서 봐야할 때는 더욱 그렇습니다. 저도 스펙은 보지 못하고 그냥 여기저기 찾아서 개발을 했습니다. OAuth는 2007년 12월에 OAuth Core 1.0 파이널 드래프트 스펙이 나왔고 2009년 6월 24일 OAuth Core 1.0 Revision A가 발표되었습니다. Beginner’s Guide to OAuth ? Part I: Overview를 보면 대략적인 내용들이 나와있는데 OAuth에 대해 이해하는데 적당히 요약하겠습니다.

사용자들은 여러가지 서비스를 쓰고 있습니다. 사진은 플리커에 쓰고 동영상은 유투브에 쓰는 등 모든 것을 통합한 사이트가 더 최적화된 기능을 제공하지 못하기 때문에 여러가지 서비스를 나누어서 쓰고 있으며 사용자들은 이들을 함께 써서 더 새로운 것을 쓰고 싶어 합니다. 그렇게 하려면 서로간에 접근을 위해서 사용자간의 개인정보(아이디, 패스워드)를 공유해야하는데 이는 보안에 좋지 않기 때문에 보통은 아이디와 비밀번호로 혼합한 키를 사용하는데 대표적인 것이 OpenID입니다. 하지만 이 키는 공유하기에는 너무 강력하고 제한이 없습니다. 또한 이것은 한번 공유된 것을 취소할 수 없어 유일하게 취소할 수 있는 키변경은 특정사이트만 막지 못하고 전체사이트에 대한 접근을 모두 막아야 합니다. OAuth는 대신 토큰을 공유하고 각 토큰은 특정 리소스와 정의된 기간에 대한 특정사이트로의 접근 권한만을 받습니다. 
(쓰고 보니 크게 도움될런지 잘 모르겠군요 ㅡ..ㅡ)
아래 이미지가 OAuth의 인증방식에 대해서 이해하기 좋게 잘 정리되어 있어서 퍼왔습니다.

Image via sitepen 
Service가 인증정보를 가지고 있는 사이트(여기서는 Twitter)이고 User가 Service의 인증정보로 Consumer사이트를 이용하려는 것입니다. 
	1. 사용자가 인증을 하려고 하면 Consumer가 Service에 토큰을 요청하고 Service가 토큰을 생성해서 돌려줍니다. 
	2. 토큰을 받은 Consumer는 User를 서비스의 인증페이지로 요청토큰과 함께 리다이렉트시킵니다.
	3. User는 Service사이트에서 인증을 하고 Service사이트는 User를 Consumer사이트로 다시 리다이렉트 시킵니다.
	4. Consumer사이트는 엑세스토큰을 서비스에 요청하여 받으면 OAuth의 인증이 완료됩니다.
	5. 이후에는 Consumer가 이 토큰을 이용해서 리소스를 Service에 요청하여 받습니다.
Twitter는 기존의 Basic Auth를 더이상 사용하지 않기로 09년 12월에 발표하고 2010년 6월에 Basic Auth는 deprecation하기로 결정했습니다. 이전에는 사용해 본적이 없어서 그전에는 정확히 어떤 절차로 진행이 되었는지 모르지만 분위기로 보아서는 그 이전에는 서드파티서비스에서 아이디와 패스워드를 직접 입력해서 트위터로그인을 하는 것이 가능했었는데 2009년 4월에 트위터는 Sign in with Twitter 기능을 추가하면서 트위터의 인증이 서드파티 사이트로 넘어가는 일이 없도록 OAuth인증을 강화했습니다. 이젠 더이상 서드파티에 직접 트위터의 아이디와 패스워드를 입력하는 것을 권장하지 않고 있습니다. 이는 보안적인 측면에서도 아주 중요한 부분이라고 생각하고 있습니다. 트위터에는 여러가지 유명한 서드파티 서비스들이 많이 좋재하지만 사용자 입장에서는 서드파티의 신뢰성을 판단하기가 쉽지 않기 때문에 그럴듯하게 사이트하나 만들어 놓고 사용자의 아이디와 패스워드를 가로챌수 있다는 의미이기도 합니다. 저도 그렇게 한번 당한적이 있어서 패스워드를 변경해 버렸더랬죠. 너무 많은 트위터 서드파티 서비스가 그런식으로 이용하고 있었기에 아무런 생각도 없이 로그인을 해버렸었습니다. ㅠ..ㅠ

트위터 클라이언트 등록하기
OAuth의 방식을 어느정도 이해했으면 이제 클라이언트 구현전에 트위터 어플리케이션 등록페이지 
에서 어플리케이션 등록을 해주어야 합니다. 어플리케이션 등록은 그냥 웹폼에서 간단하게 등록할 수 있습니다. 나중에 트위터 클라이언트에서 트윗을 작성했을 때 표시되는 클라이언트이름을 이곳에서 지정해 주게 되고 데스크탑 클라이언트인지 웹서비스인지를 선택해서 등록을 하면 Consumer key와 Consumer secret를 발급받을 수 있고 OAuth인증을 할때 사용합니다. 데스크탑 클라이언트는 만들어보지 않았지만 데스크탑클라이언트로 등록하면 PIN번호라는 것을 발급받게 되는 것 같습니다.

글이 길어져서 둘로 나눕니다. 이 포스팅은  Twitter4j로 트위터 사용하기 #2로 이어집니다. 

Twitter4j사이트의 Code Example 에 간단한 예제가 나와있어서 참고하면 되지만 너무 심플한 예제라 큰 도움은 되지 않습니다. 차라리 JavaDoc 을 많이 보게 되더군요.



인증토큰 얻기
Twitter4J를 사용하려면 당연히 최신버전의 Twitter4J jar파일을 프로젝트에 추가하여 하고 해당 소스를 사용할때 당연히 import도 해야하지만 그런부분은 여기서는 생략하고 소스만 보겠습니다. ㅎ

?
1	final String CONSUMER_KEY = "발급받은 CONSUMER Key";
2	final String CONSUMER_SECRET = "발급받은 CONSUMER Secret 키";
3	 
4	Twitter twitter = new Twitter();
5	twitter.setOAuthConsumer(CONSUMER_KEY, CONSUMER_SECRET);
6	 
7	RequestToken requestToken = null;
8	try {
9	   requestToken = twitter.getOAuthRequestToken();
10	} catch (TwitterException e) {
11	}
12	//store requestToken.getToken() & requestToken.getTokenSecret()
13	//Retirect to requestToken.getAuthorizationURL()
위 코드를 통해서 토큰을 얻을 수 있습니다. requestToken.getToken()과 requestToken.getTokenSecret()에서 스트링타입의 토큰을 트위터로부터 받아오게 되고 사용자가 트위터사이트에서 인증을 허락한 뒤에 다시 사용해야 하므로 세션등에 저장해 둡니다. requestToken.getAuthorizationURL()는 트위터 인증URL에 토큰을 파라미터로 넘겨주는 주소로 다음과 같은 형태입니다.

http://twitter.com/oauth/authorize?oauth_token=인증토큰

위의 URL을 이용해서 유저를 리다이렉트 시키면 아래와 같은 화면이 나오게 됩니다.

제가 만들때는 구조상 아이프레임내에서 처리해야 했기 때문에 위 페이지를 아이프레임에서 띄웠습니다만 저 페이지에는 (window.top !== window.self)와 같이 페이지가 프레임에서 띄워졌는지를 검사하는 코드가 있고 프레임일 경우는 전체페이지에 띄우도록 수정해 버립니다. 이부분은 꼼수를 쓰면 막을수 있을지도 모르겠지만 프레임에서 띄우면 사용자가 URL을 볼수가 없기 때문에 트위터와 동일한 모양의 페이지를 만들어 놓고 아이디와 패스워드를 가로챌 수 있는 보안상의 문제가 있기 때문에 굳이 프레임에서 띄우지 않고 새창에서 인증이 진행되도록 하였습니다. OAuth도 인증과정은 유저에게 맡기기 때문에 URL을 사용자에게 표시해 주는 것은 중요합니다.

이제 사용자가 트위터사이트에서 해당 클라이언트의 접근을 허락할것인지 거절할 것인지를 선택합니다. 거절하게 되면 당연히 트위터의 인증을 하지못하게 되고 Allow를 하게되면 트위터가 사용자를 다시 Consumer사이트로 리다이렉트 시키게 됩니다.

http://리다이렉트URL?oauth_token=인증토큰

리다이렉트URL은 트위터 어플등록을 할 때 입력했던 URL을 이용해서 발급했던 인증토큰을 다시 파라미터로 붙혀서 보내주게 되고 파라미터명은 oauth_token입니다. 리다이렉트 페이지에서 해당 토큰을 다시 받아서 인증처리를 해주면 됩니다.



인증하기
?
1	Twitter twitter = new Twitter();
2	twitter.setOAuthConsumer(CONSUMER_KEY, CONSUMER_SECRET);
3	 
4	String oauthToken = 파라미터로 받은 oauth_token
5	if (저장된token.equals(oauthToken)) {
6	   try {
7	       accessToken = twitter.getOAuthAccessToken(oauthToken, 저장된serectToken);
8	   } catch (TwitterException e) {
9	   }
10	 
11	   twitter.setOAuthAccessToken(accessToken);
12	 
13	    //store oauthToke & secretToken to DB
14	}
받아온 oauth_token값과 앞단계에서 발급받은 토큰의 값을 기뵤해서 값을 경우에 2개의 값(token, serect token)으로  accessToken을 만들어서 twitter객체가 OAuth권한을 얻도록 합니다. 여기까지 진행되면 twitter객체를 이용해서 해당 유저의 트위터를 이용할 수 있게 됩니다. 첫 토큰획득과 2번째 비교할때의 시간텀이 길어지게 되면 트위터에서 인증을 거부합니다.

일시적인 인증이 아니라면 Token과 Secret Token을 디비에 저장해 두면 다음에 사용자가 로그인 했을 경우에도 다시 트위터의 접근 권한을 자동으로 얻을 수 있습니다.

?
1	Twitter twitter = new Twitter();
2	twitter.setOAuthConsumer(CONSUMER_KEY, CONSUMER_SECRET);
3	 
4	AccessToken accessToken = null;
5	accessToken = new AccessToken(저장된Token, 저장된SecretToken);
6	twitter.setOAuthAccessToken(accessToken);
위 코드처럼 2개의 토큰을 이용해서 twitter객체가 다시 인증된 상태로 만들면 됩니다. 이 twitter객체를 세션등에 저장해 놓고 계속 사용하면 됩니다. 그리고 트위터는 인증을 할때 유저의 스크린네임을 돌려주기 때문에 accessToken.getScreenName()를 이용하면 인증하면서 바로 스크린 네임을 얻을 수 있습니다. 



트윗 가져오기
?
1	List<Status> statuses;
2	 
3	Paging page = new Paging();
4	page.count(20);
5	page.setPage(1);
6	 
7	try {
8	   statuses = twitter.getHomeTimeline(page);
9	} catch (TwitterException e) {
10	}
11	 
12	for (Status status : statuses) {
13	   //status.getId()
14	   //status.getUser().getName() 
15	   //status.getUser().getScreenName() 
16	   //status.getUser().getURL()
17	   //status.getText()
18	   //status.getCreatedAt()
19	   //status.getUser().getProfileImageURL()
20	   //status.getSource()
21	}
페이징이 필요할때는 Paging객체 를 만들어서 사용하면 되고 사용자의 타임라인은 getHomeTimeline 
을 이용하여 얻습니다. 각 트윗에 대한 정보는 status객체 를 통해서 얻어낼수 있고 사용자 정보는 User객체 를 통해서 추가적으로 얻을 수 있습니다. 멘션이나 Direct Message는 getMentions, getDirectMessages를 통해서 가져올 수 있습니다. 

트윗작성하기
?
1	Status status = null;
2	try {
3	   status = twitter.updateStatus(텍스트);
4	} catch (TwitterException e) {
5	}
트윗을 올리는 것은 아주 간단합니다. updateStatus메서드를 이용해서 텍스트를 전송하면 바로 트윗이 올라갑니다. Reply의 경우에는 twitter.updateStatus(텍스트, 리플라이할 트윗의 id); 와 같은 형태로 사용하면 됩니다.
이외에도 Twitter4j에서는 많은 기능을 제공하고 있고 거의 모든 트위터의 기능을 아주 쉽게 사용할 수 있게 잘 작성되어 있습니다. 저도 쓰는거만 만져보고 다 보지는 못했네요.
