---
title: "Missing contentDescription attribute on image"
categories: 
  - android
toc: true
---

## Missing contentDescription attribute on image
  
안드로이드 앱 xml 레이아웃 확인 중 아래와 같은 경고가 떴다
Missing contentDescription attribute on image 

이미지 xml 에 contentDescription를 추가해달라는거다. (이미지 인식이 힘든 사회적 약자를 위해 넣어주는게 가장 좋겠지만.. 애매할때가 좀 있다) 이것을 무시하려면 아래와 같이 넣어주면된다.
  
```xml
tools:ignore="ContentDescription"
```

문장에서 알 수 있듯이 ContentDescription WARNING을 무시해주는것이다.  