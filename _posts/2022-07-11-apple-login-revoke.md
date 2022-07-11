---
title: "Apple login. revoke api"
categories: 
  - ios
toc: true
---
  
## Apple login revoke api
  
아이폰, 아이패드용 앱에 SNS 로그인을 기능이 있으면 애플 로그인을 넣어야 심사가 통과된다.  
그리고 애플 정책상 회원가입 로그인이 있으면 탈퇴 기능이 앱안에 있어야 하며 애플 로그인 관련된 토큰을 삭제하는 api 도 호출시켜야 한다고 한다.  
아래는 정책 내용 링크이다.  
  
[https://developer.apple.com/kr/support/offering-account-deletion-in-your-app](https://developer.apple.com/kr/support/offering-account-deletion-in-your-app)
  
현재 적용하려는 앱은 웹에서 애플로그인 처리를 한다. (js를 이용한 방식)
  
그리고 revoke api 는 아래 링크로 문서가 제공된다.  
  
[https://developer.apple.com/documentation/sign_in_with_apple/revoke_tokens](https://developer.apple.com/documentation/sign_in_with_apple/revoke_tokens)  

처음보면 좀 당황스럽다.  

작성해야 하는 내용은 아래와 같다.  

```
POST https://appleid.apple.com/auth/revoke
client_id
client_secret
token
```

client_id : 애플 개발자 사이트에 Service Id에 작성되 있는 Identifier.  
client_secret : JWT 토큰이다. p8 파일로 사이닝하며 ES256 알고리즘을 이용해야한다.  
token : 로그인 후 애플 서버를 통해 얻어오는 access token or refresh token 이다.  
  
  
여기서 **client_secret**을 만들기 위해서는 아래 링크의 Create the client secret 부분을 참고해야한다.

[https://developer.apple.com/documentation/sign_in_with_apple/generate_and_validate_tokens](https://developer.apple.com/documentation/sign_in_with_apple/generate_and_validate_tokens)
  
아래는 파이선으로 만들어본 client_secret이다.  
client_secret는 JWT이며 p8파일로 사이닝을 한다. 알고리즘은 ES256으로 해야함.

```
    headers = {
       'kid': "p8 파일 만들었을때 Key ID"
    }

    payload = {
        'iss': "팀 네임",
        'iat': timezone.now(),
        'exp': timezone.now() + timedelta(days=150),
        'aud': 'https://appleid.apple.com',
        'sub': Service Id에 작성되 있는 Identifier,
    }

    client_secret = jwt.encode(
        payload, 
        '''-----BEGIN PRIVATE KEY-----
p8 파일안에 내용을 넣으면 된다.
-----END PRIVATE KEY-----''', 
        algorithm='ES256', 
        headers=headers
    )
```
  
JWT 형식으로   
xxxxx.xxxxx.xxxxxxx  
뭐 이런식으로 결과값이 나온다. **client_secret**을 만들었다.
  
다음 파라미터인 **token**을 얻기위해서는 아래와 api을 이용한다. 

작성해야 하는 내용은 아래와 같다.

```
POST https://appleid.apple.com/auth/token

client_id
client_secret
code
grant_type
redirect_uri
```

여기서 client_id, client_secret는 위에서 사용했던 내용을 똑같이 사용해도 되고  
code 파라미터는 apple login 후에 https://appleid.apple.com/appleauth/auth/oauth/authorize or redirect url의 body에 "grant_code": xxxx.xxxx.xxxxx로되어 있는것을 이용한다.  
grant_type은 authorization_code라고 넣으면 된다.  
redirect_uri은 애플 개발자 사이트에서 로그인 후 이동하는 url을 넣었던 내용을 넣으면된다.  
각파라미터에 대한 설명은 아래와 같다.  
  
```
client_id: Service Id에 작성되 있는 Identifier
client_secret: 위에서 만든 client_secret
code: 로그인 후 받아온 body의 ("grant_code": xxxx.xxxx.xxxxx)
grant_type: "authorization_code"
redirect_uri: 콜백 받을 url
```
  
이 api를 이용하면 access_token과 refresh_token을 얻어올 수 있다.  
이 두 토큰 값이 https://appleid.apple.com/auth/revoke api의 token 값이다.  
  
이제 이 파라미터를 이용하면 정상적으로 revoke이 되는것을 확인할 수 있다.  
하지만 api를 통해서는 확인이 안되니 아래 사이트에 들어가서 로그인해 확인해야한다.  
[https://appleid.apple.com/](https://appleid.apple.com/)
  
끝~  
