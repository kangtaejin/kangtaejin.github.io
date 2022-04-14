---
title: "fastlane github runner: self-host"
categories: 
  - ios
toc: true
---

## fastlane github runner: self-host
  
ios 배포를 위해 Fastlane은 구성을 완료했고 github action을 통해 배포를 하려고 할때 선택지는 두가지가 있다.  
깃허브 액션의 runs-on을 맥, 윈도우, 리눅스 중 하나를 선택해 자원을 사용하는 방법과 깃허브 runner를 이용해 self-hosted를 이용하는 방법이다.  
  
깃허브 액션의 mac os 경우 비싸서 사용하기 부담스러웠다. 그래서 self-hosted를 이용하기로 했다.  
self-hosted의 단점으로는 사용될 runner의 mac이 필요하며 runner 프로그램이 켜져있어야 한다.  
  
평소에 Fastlane을 이용했다면 자신의 로컬환경 터미널에서 Fastlane '실행할 lane 이름'을 이용해 빌드를 할 수 있다.  
그래서 Github actions의 steps를 checkout 과 fastlane 명령어로 이용하면 될거라 생각했으나 처음엔 빌드 실패했다.  
이유는 cocoapods 가 이유였으며 Fastlane 파일에 cocoapods(use_bundle_exec: false) 을 추가해 빌드 성공했다.  
  
생각보다 간단했으며 평소 테스트 서버, 스테이징 서버, 릴리즈 서버를 테스트 플라이트에 올리는 번거로운 작업을 깃허브 PR 시 자동으로 테스트 플라이트에 올리는 방법으로 전환했다.  
  
맥에서 깃허브 runner run.sh 파일을 자동으로 실행하기 위해서는 맥 프로그램인 Automator를 이용해 .sh 파일을 실행하는 응용프로그램을 만들수 있었다.  
이 응용프로그램을 시작프로그램으로 등록하면 되는데 시스템 환경설정 > 사용자 및 그룹 > 로그인 항목에서 +버튼을 이용해 등록된 응용프로그램을 추가하면된다.  
