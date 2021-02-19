---
title: "android okhttp minSdkVersion issue"
categories: 
  - android
toc: true
---

## okhttp 3.13 Android 5+

Retrofit 라이브러리와 함께 자주 사용되는 okhttp가 업데이트 되면서 minSdkVersion이 19->21로 올라갔다.
19사용자는 크래시나면서 죽는 경우가 있음.
분기가 되는 버전은 3.12.x 버전까지는 minSdkVersion이 19이고
그 이상은 minSdkVersion이 21이다.
  
자세한 내용은 아래 링크에 있다.
  
<https://developer.squareup.com/blog/okhttp-3-13-requires-android-5/>
  
3.12 이하 버전을 사용해도 되지만 보안상 문제로 올리는게 맞는듯.
19이하 사용자가 좀 있는것 같으나 슬슬 minSdk를 21로 맞춰도 되는 시기가 온것같다.