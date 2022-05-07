---
title: "Flutter IOS CocoaPods not installed. Skipping pod install..."
categories: 
  - ios
toc: true
---

mac os 업데이트하고 플러터 IOS를 안드로이드 스튜디오에서 빌드하려고 하니 코코아팟 설치가 안되어 있다고 메시지를 보여줬다.  
  
혹시나 하고 터미널에서 확인해보니 코코아팟은 정상설치되어 있었으나 flutter doctor로 확인해보니 안드로이드 스튜디오에서 확인이 되지 않았다.  
  
구글링 해보니 코코아팟을 다시 설치해보라고 해서 다시 설치했으나 해결하지 못했고  
  
안드로이드 스튜디오에서 file -> invalidate cache / restart 을 이용해보라고 해서 해봤으나 해결하지 못했다.  
  
좀더 구글링해보니 안드로이드 스튜디오를 끄고 터미널에서 
  
```
open /Applications/Android\ Studio.app 
```
  
으로 앱을 실행시켜보라고 해서 실행시켜봤더니 코코아팟설치된걸 인식하고 있었다.  
  
뭐지..  
  
하지만 이거저거 막 만졌는지 빌드하려고 하니  
CocoaPods's specs repository is too out-of-date to satisfy dependencies...  
뭐 이런 메시지가 나오며 안되었다.  
ios의 Podfile.lock을 지우고 다시 빌드해보니 성공했다.  
  
끝
