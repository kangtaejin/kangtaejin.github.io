---
title: "Android 12 대략적인 위치 권한"
categories: 
  - android
toc: true
---
  
## Android 12 대략적인 위치 권한 이슈
  
targetSdk를 31로 설정하니 Android 12에서 위치 권한에 변경사항이 있었다.  
대략적인 위치 권한을 사용자가 선택할수 있게 바뀌었다.  
지도를 이용한 앱의 경우 대략적인 위치로 내위치를 사용할 경우 오차로 불편함을 느낄수 있는데  
대략적인 위치 권한을 정확한 위치 권한으로 다시 묻고 싶을때가 있다.  
이때 Activity에 있는 requestPermissions을 사용할 경우 다시 묻지 않는다.  
  
그럴때 간단하게 ActivityCompat.requestPermissions을 사용하면 대략적인 위치 권한을 선택했을 경우 다시 권한을 물을수 있게된다.  
