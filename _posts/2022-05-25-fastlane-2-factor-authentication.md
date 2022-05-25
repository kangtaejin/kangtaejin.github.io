---
title: "Fastlane Apple 2-factor authentication"
categories: 
  - ios
toc: true
---

Github action self hosted를 이용해 Fastlane IOS 빌드해 TestFlight에 올리고 있었다.  
잘되다가 갑자기 로그인 인증이 되지 않는다고 TestFlight에 올리는것이 실패했다.  
  
애플의 2-factor 인증때문에 생긴일이었다.  

```
fastlane spaceauth -u user@email.com
```

위와 같이 이용하면 2 factor인증하도록 도와주는데 인증번호를 넣고 인증하면 Fastlane을 이용하는데 문제가 없다.  
하지만 주기적으로 인증이 풀려 불편하다.  
보안상 풀리는게 맞나 싶기도...  
  
관련문서  
<https://docs.fastlane.tools/getting-started/ios/authentication/>
