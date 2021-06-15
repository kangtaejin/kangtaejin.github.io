---
title: "Task :app:uploadCrashlyticsMappingFileRelease FAILED"
categories: 
  - android
toc: true
---

## Task :app:uploadCrashlyticsMappingFileRelease FAILED
  
Gradle 버전을 올리고 나서 갑자기 gradle을 통한 빌드 실패를 했다.
  
오류메시지는 아래 부분에서 실패했었다.
  
Task :app:uploadCrashlyticsMappingFileRelease FAILED
  
이전엔 잘되었었는데 왜지... 싶어서 구글링해보니 gradle에 파이어베이스 플러그인 순서를 바꿔주면 된다고 한다.
  
이전  
  
```gradle
apply plugin: 'com.google.firebase.crashlytics'
apply plugin: 'com.google.gms.google-services'
```
  
이후
  
```gradle
apply plugin: 'com.google.gms.google-services'
apply plugin: 'com.google.firebase.crashlytics'
```
  
이렇게 순서를 바꿨더니 해결되었다