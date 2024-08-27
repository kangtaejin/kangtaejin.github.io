---
title: "Godot Rider, VSCODE - godot files have been modified on disk"
categories: 
  - Godot
toc: true
---
  
## Godot Rider, VSCODE - godot files have been modified on disk
  
Godot은 C#도 지원하는데 Godot안에 있는 에디터로는 C#코딩하기 쉽지 않다.  
그래서 Jetbrain의 Rider를 외부 에디터로 사용할 수 있다.  
아마도 Rider 뿐만 아니라 VSCODE경우도 같은 현상일거라고 예상한다.  
외부 에디터에서 코드를 수정하고 다시 저장하려고하면 Godot에서 아래와 같은 메시지를 보여준다. (Godot 한글 버전을 쓰고 있다.)  
files have been modified on disk  
뭐 이런 메시지 후에 기존 파일을 저장해서 쓸래 아니면 다시 복구할래 같은 선택할수 있게 해주는데 나같은 경우는 정상동작하지 않았고
매번 CS파일을 작성 및 수정할때마다 저 창을 보고 싶지 않았다.  
해결방법은 Godot 상단 메뉴 > 에디터 설정 > 텍스트 에디터 > 행동 > 파일 > 외부에서 변경 시 스크립트 자동 새로고침 을 사용으로 켜줬다.  
이러니 문제 없이 해결되었다.  
이러한 질문 답이 Reddit에는 존재하나 영어버전 메뉴라 한글버전으로 작성했다.  