---
title: "IOS FCM을 이용한 푸시에서 Xcode에서는 정상작동하나 TestFlight에서 정상작동하지 않을때"
categories: 
  - ios
toc: true
---

## IOS FCM을 이용한 푸시에서 Xcode에서는 정상작동하나 TestFlight에서 정상작동하지 않을때

ios에서 푸시 서비스를 FCM를 이용해 구현했다.  
  
Xcode로 빌드해서 폰에 넣어서 테스트하면 푸시가 정상으로 수신되었는데  
TestFlight에 올리거나 앱스토어에 올려서 확인해보니 푸시가 정상동작하지 않았다. (푸시 수신하지 않음)    
  
찾아보니 FCM 라이브러리 몇몇 버전에서 문제가 있는 버전이 있다고 한다.  
가능한한 최신버전을 사용하는게 좋으나 이런 문제가 있을땐 좀 조심스러워 진다.  
아래 버전은 큰 문제가 없었다.

```
  pod 'Firebase/Messaging', '~> 7.1.0'
```
