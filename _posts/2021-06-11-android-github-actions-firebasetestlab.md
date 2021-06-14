---
title: "Android github actions and firebase testlab"
categories: 
  - android
toc: true
---

## Android github actions and firebase testlab

깃허브 액션와 파이어베이스 TestLab 서비스를 연동하는 작업을 하려는데 참고한 글은 아래와 같다.
  
<https://medium.com/firebase-developers/github-actions-firebase-test-lab-4bc830685a99>  
  
스크립트 작성하고 동작이 잘되는것을 확인했다.
  
물론 저 글대로 작성하지는 않았고
Pull Request 이벤트가 발생하면 
빌드 후 파일을 남기지 않고 바로 TestLab에 올려 UI테스트 결과를 볼수 있게 했다.
  
하지만 아래 Github action이 deprecated 되었다고 나온다.
  
uses: GoogleCloudPlatform/github-actions/setup-gcloud@master
  
그리고 친절하게   
<https://github.com/google-github-actions/setup-gcloud>  
이걸 이용하라고 해서 다시 google-github-actions으로 작성 다시해보니
별문제 없이 잘되었다.  
  
UI Robo테스트가 얼마나 나중에 효율적일지는 모르겠지만
테스트는 많이해서 나쁠거는 없으니..
  
자동화했다는 점에서 마음에 들었다.
