---
title: "Expecting android:screenOrientation="unspecified" or "fullSensor" for this activity so the user can use the application in any orientation and provide a great experience on Chrome OS devices"
categories: 
  - android
toc: true
---

## Expecting android:screenOrientation="unspecified" or "fullSensor" for this activity so the user can use the application in any orientation and provide a great experience on Chrome OS devices
  
앱 개발하다보면 앱 레이아웃을 portrait으로 강제하고 개발하는 경우가 많은데
android studio inspection에서 아래 메시지를 보여준다 

Expecting android:screenOrientation="unspecified" or "fullSensor" for this activity so the user can use the application in any orientation and provide a great experience on Chrome OS devices

portrait으로 강제하지 말라는거 같은데 이 경고 메시지가 보기 싫다면 
AndroidManifest.xml에 아래와 같이 추가해주면 된다.
  
```xml
tools:ignore="LockedOrientationActivity"
```
