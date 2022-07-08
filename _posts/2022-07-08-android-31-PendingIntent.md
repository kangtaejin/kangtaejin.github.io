---
title: "Android TargetSdk 31 PendingIntent"
categories: 
  - android
toc: true
---
  
## Android TargetSdk 31 PendingIntent
  
Android TargetSdk를 31로 설정하고 나서 크래시리틱스에 들어온 에러가 있었는데 아래와 같았다.  
  
```
Fatal Exception: java.lang.IllegalArgumentException
com.mediawill.serve: Targeting S+ (version 31 and above) requires that one of FLAG_IMMUTABLE or FLAG_MUTABLE be specified when creating a PendingIntent. Strongly consider using FLAG_IMMUTABLE, only use FLAG_MUTABLE if some functionality depends on the PendingIntent being mutable, e.g. if it needs to be used with inline replies or bubbles.
```
  
내용은 PendingIntent를 이용할때 Flag를 FLAG_IMMUTABLE or FLAG_MUTABLE를 주라는 말이다.  
이 룰을 지키지 않으면 크래시가 나는 모양이다.  
  
나같은 경우는 푸시를 이용할때 PendingIntent를 이용했는데
Android S 이상일때 FLAG_IMMUTABLE를 이용해 분기처리하였다.
