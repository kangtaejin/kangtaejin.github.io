---
title: "Android github actions and firebase distribution"
categories: 
  - android
toc: true
---

## Android github actions and firebase distribution

github action를 통해 파이어베이스 distribution 기능을 사용할 수 있다.  
즉 깃의 Push나 Pull Request 시 빌드해 테스터에게 aab or apk를
IOS Testflight처럼 편리하게 진행할수 있다.  
빌드가 번번하게 일어날 경우 2000분을 넘게되면 유료이니 무료 사용자들은 주의할 필요가 있다.
  
처음에는 깃허브 마켓플레이스의 아래를 이용하려고 했으나 apk 파일은 되는데 aab파일이 진행되지 않았다.  
(물론 제가 잘 못한걸 수도...)  
https://github.com/marketplace/actions/firebase-app-distribution  
(아마도 추후엔 지원할 가능성이 높을것 같다)

aab파일은 아직 지원하지 않는다는 이야기가 있었으나 최근에 지원하는 것을 확인했고  
파이어베이스 CLI를 확인하여 해보니 문제없이 업로드가 되었다.  
https://firebase.google.com/docs/app-distribution/ios/distribute-cli  
  
    
성공한 액션 yml은 아래와 같다.

```
name: Build & upload to Firebase App Distribution 

on: 
  pull_request:
    branches:
      - develop

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v1
    - uses: actions/setup-node@v1 # This is optional on linux and macOS
    - uses: pocket-apps/action-setup-firebase@v2
      with:
        firebase-token: ${{secrets.FIREBASE_TOKEN}}
    - name: set up JDK 1.8
      uses: actions/setup-java@v1
      with:
        java-version: 1.8
    - name: Make gradlew executable
      run: chmod +x ./gradlew

    - name: build debug 
      run: ./gradlew bundleDebug
    - name: upload debug artifact to Firebase App Distribution
      run: firebase appdistribution:distribute app/build/outputs/bundle/debug/app-debug.aab --token ${{secrets.FIREBASE_TOKEN}} --app ${{secrets.FIREBASE_APP_ID}} --groups "trusted-testers" --release-notes "Test server"

    - name: build stage 
      run: ./gradlew bundleStage
    - name: upload stage artifact to Firebase App Distribution
      run: firebase appdistribution:distribute app/build/outputs/bundle/stage/app-stage.aab --token ${{secrets.FIREBASE_TOKEN}} --app ${{secrets.FIREBASE_APP_ID}} --groups "trusted-testers" --release-notes "Stage server"
      
    - name: build release 
      run: ./gradlew bundleRelease
    - name: upload release artifact to Firebase App Distribution
      run: firebase appdistribution:distribute app/build/outputs/bundle/release/app-release.aab --token ${{secrets.FIREBASE_TOKEN}} --app ${{secrets.FIREBASE_APP_ID}} --groups "trusted-testers" --release-notes "Release server"

    - name: action-slack
      uses: 8398a7/action-slack@v3.8.0
      with:
        status: ${{ job.status }}
        fields: repo,message,commit,author,action,eventName,ref,workflow,job,took
      env:
         SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK_URL }}
```

빌드 서버 구성이 디버그, 스테이지, 운영서버 이렇게 빌드되고 있으며
  
과정은  
  
소스체크아웃  
파이어베이스 설치 및 토큰 인증  
자바설치  
Gradle 권한 추가  
소스 빌드 후 Distribution  
슬랙에 알리기  
  
깃헙 시크릿은 이름이 설명과 같아 크게 설명할게 없다..
FIREBASE_TOKEN 파이어베이스 로그인 후 토큰값
FIREBASE_APP_ID 파이어베이스 앱아이디
SLACK_WEBHOOK_URL 슬랙 웹훅

완성했다면 아래와 같은 진행을 할 수 있을듯하다  
  
feature branch -> develop branch pull request  
actions -> build -> firebase app distribution -> slack or email for testers  
test -> develop branch merge  

