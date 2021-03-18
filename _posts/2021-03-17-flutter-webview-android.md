---
title: "flutter android webview net::ERR_CACHE_MISS"
categories: 
  - flutter
toc: true
---

## flutter android webview net::ERR_CACHE_MISS
  
요즘 플러터를 공부하고 있다.

웹뷰를 이용해서 웹페이지를 보여주는 기능을 공부하고 있다.
(https://pub.dev/packages/webview_flutter)

이상하게도 첫페이지는 잘보여주는데 눌러서 이동하려고하면 아래와 같은 에러를 보여주며 제대로 url이동이 되지 않았다.
  
net::ERR_CACHE_MISS
  
난 당연히 웹의 첫페이지가 잘보여지길래 퍼미션문제는 아닐거라고 생각했는데 퍼미션 문제가 맞았다.
  
AndroidManifest에 인터넷 권한을 추가해주면된다.
  
```xml
<uses-permission android:name="android.permission.INTERNET"/>
```