---
title: "Avoid using android.media.ExifInterface; use android.support.media.ExifInterface from the support library instead"
categories: 
  - android
toc: true
---

## Avoid using android.media.ExifInterface; use android.support.media.ExifInterface from the support library instead
  
안드로이드 앱 소스 리팩토리중 아래와 같은 경고가 떴다
Avoid using android.media.ExifInterface; use android.support.media.ExifInterface from the support library instead 

라이브러리 임포트를 다른것을 하라는것이었는데 시키는대로 android.support.media.ExifInterface을 했더니 못찾았다.
대신 아래 것을 사용하면 되었다.
  
```kotlin
import androidx.exifinterface.media.ExifInterface
```
