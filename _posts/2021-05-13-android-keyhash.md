---
title: "android key hash"
categories: 
  - android
toc: true
---

## android keytool. keystore key hash.

안드로이드 개발을 키 해시값을 얻을 필요가 있을때가 있다.
뒤에 =이 붙는 형태이다.
  
보통 붙여넣기해서 사용하기에 블로그에 적어둔다.
keytool위치는 android tools 쪽을 보면 있다.
터미널이나 cmd를 이용하면 된다.
  
맥 디버그 용
```
keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore -storepass android -keypass android | openssl sha1 -binary | openssl base64
```
  
맥 릴리즈 용
```
keytool -exportcert -alias <RELEASE_KEY_ALIAS> -keystore <RELEASE_KEY_PATH> -storepass <STORE_PASSWORD> -keypass <KEY_PASSWORD> | openssl sha1 -binary | openssl base64
```
  
윈도우 릴리즈 용
```
keytool -exportcert -alias <RELEASE_KEY_ALIAS> -keystore <RELEASE_KEY_PATH> | openssl sha1 -binary | openssl base64
```
  
PlayStore sha-1값
```
echo <PlayStore SHA-1> | xxd -r -p | openssl base64
```
  
Android Studio SigningReport 에서 얻은 SHA1 값
```
echo <SigningReport SHA-1> | xxd -r -p | openssl base64
```