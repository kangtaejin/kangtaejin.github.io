---
title: "unity3d ios admob"
categories: 
  - unity3d
toc: true
---

## unity3d ios admob -ObjC
  
유니티에서 애드몹을 넣고 빌드 후에 Xcode에서 열어서 빌드를 해보니 앱이 죽는 문제가 있었다. 크래시 로그를 보니 해결방법이 있었다.
  
빌드세팅에서 Linking의 Other Linker Flags에 -ObjC 옵션을 추가해줘야한다.
  
빌드할때마다 Xcode에서 저 세팅을 해줘야한다니.. 유니티에서 세팅해주는 방법은 없는걸까.. 빌드를 자주하게 되는데 번거롭다.