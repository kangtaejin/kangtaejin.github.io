---
title: "Flutter Admob 화면 깜빡임 현상 (flickering)"
categories: 
  - flutter
toc: true
---

## Flutter Admob 화면 깜빡임 현상 (flickering)
  
기존에 존재하던 플러터 프로젝트를 플러터 최신버전으로 바꿔 빌드를해 앱업데이트를 하고 싶어져 flutter SDK를 stable 2.8.1 버전을 받아 적용해봤다.  
바뀐게 많지 않아 빌드하는데는 문제 없었으나 테스트 중 이상한점을 발견했다.  
화면 전환시에 화면이 깜빡이는 현상이 발생하였다.  
원인을 찾던 중 애드몹 하단 배너를 주석처리해보니 정상동작했다.  
  
애드몹 플러그인을 사용했었는데 깃헙 주소는 아래와 같다.  
<https://github.com/googleads/googleads-mobile-flutter>
  
  
이슈를 뒤져보니 역시나 나랑 비슷한 문제를 가지고 있다는 글이 있었고 Flutter SDK 버전이 올라가길 기다려야한다는 글이 있었다.
이슈링크는 아래와 같다.
<https://github.com/googleads/googleads-mobile-flutter/issues/467>
  
물론 이전버전을 사용해서 다시 빌드를 하면 문제가 해결된다. 하지만 뭔가 찝찝하고 급한일도 아니니 결국 앱업데이트는 다시 안정된 SDK를 가디라는 것으로 결론은 내고 다음 flutter SDK stable 버전을 기다리기로 마음을 먹었다.

