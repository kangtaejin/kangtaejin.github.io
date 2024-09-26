---
title: "viewpager 양쪽 뷰 살짝 보이게 하기"
categories: 
  - android
toc: true
---

## viewpager 양쪽 뷰 살짝 보이게 하기

viewpager를 자주 쓰게 되는데 이미지를 넘어가듯 보여줄때도 사용하게 된다.  
그런데... 살짝 좌우가 보이도록 UI를 구성하려고 하는데  
  
처음 생각은 오픈소스 없나 찾아봤는데 마땅히 없더라...  
그래서 구글링 해보니 viewpager 설정을 살짝만 해주면 좌우가 미리 보이는 viewpager를 만들 수 있었다.  
  
설정값은 아래와 같다.
  
```java
mViewPager.setClipToPadding(false);

mViewPager.setPadding(40,0,40,0);
```
  
  
setpadding의 첫번째 세번째 파라미터는 그만큼 좌우 보이게 한다는 설정...  
참 간단히 설정은 되나 첫번째 뷰일경우 좌측의 이미지가 보이지 않아서 빈공간으로 보이더라...  
이부분은 자연스럽게 처리할 고민을 할 필요는 있겠다.  