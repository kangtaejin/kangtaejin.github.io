---
title: "Ios xcode archive multiple commands produce Error"
categories: 
  - Ios
toc: true
---
  
## Ios xcode archive multiple commands produce Error
  
IOS에서 deploytarget을 10에서 14로 올린 프로젝트가 있었는데  
Xcode 상에서 run을 했을시에는 문제가 없다가 빌드해서 테스트플라이트로 올리려했더니  
multiple commands produce.... 이런 에러가 났다.  
  
문제의 원인은 cocoapods를 이용하는데 notification 관련 타겟이 나눠져 있는 상태에서  
notification deployment target은 10에서 14로 올리지 않아 10으로 설정되어 있었다.  
  
그래서 cocoapods에서 중복된 라이브러리를 가져올때 두가지 버전의 가져오게되어 문제가 생긴것으로 보였다.  
해결방법은 간단했다. 타겟이 나눠진 경우 나눠져있는 deployment target도 동일하게 14로 맞추면 되었다.  
  
어찌보면 간단한 실수였는데 당황하여 시간을 좀 허비하였다.  