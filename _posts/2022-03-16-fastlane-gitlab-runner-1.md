---
title: "fastlane gitlab runner - 1"
categories: 
  - android
  - ios
toc: true
---

## fastlane gitlab runner - 1
  
gitlab cicd을 이용해 자동배포를 위해 fastlane을 사용하기로 했다.  
android/ios 동시에 구성하기에 fastlane이 편해보였기 때문이다.  
설치형 깃랩의 경우 리눅스환경에서 설치되어 ios에서 자체 빌드는 하기 힘들고 gitlab runner를 이용해 mac에서 빌드하도록 하면 되겠지.. 하고 시작해봤다.  
  
ios와 android를 동시에 빌드하기 위한 구성할 runner의 OS은 mac이다.  
먼저 Gitlab 프로젝트에서 runner를 등록해야한다.  
  
Gitlab Runner 설정  
깃랩프로젝트로 들어가서 Settings > CICD 메뉴를 들어간다.  
Runner 의 가장 오른쪽에 Expand 버튼을 누르면 설정 화면이 보인다.  
설정하는데 Set up a specific runner manually 의 아래 두 값을 이용해 로컬 PC (러너로 돌릴 PC) 등록이 필요하다.  
Register the runner with this URL  // 등록 URL  
And this registration token  // 등록 토큰  
  
만약 등록이 완료되었다면 하단에 Available specific runners에 자신의 PC가 떠 있는것을 확인할수 있다.  
필요한 정보는 다 구했으니 로컬 PC (러너로 돌릴 PC)를 설정해보자.  
사실 mac에서 설정하는 방법은 이 문서를 볼것도 없이 Show Runner installation instuctions를 보면 잘나와 있다.  
  
다운로드  
```
# Download the binary for your system
sudo curl --output /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-darwin-amd64

# Give it permissions to execute
sudo chmod +x /usr/local/bin/gitlab-runner

# The rest of commands execute as the user who will run the Runner
# Register the Runner (steps below), then run
cd ~
gitlab-runner install
gitlab-runner start
```
  
실행  
```
sudo gitlab-runner register --url 등록URL --registration-token 등록토큰
```
