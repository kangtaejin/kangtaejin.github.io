---
title: "Ios xcode cocoapods to spm error framework not found"
categories: 
  - Ios
toc: true
---
  
## Ios xcode cocoapods to spm error framework not found
  
IOS에서 cocoapod 대신 이제 spm을 주로 사용하는 분위기인것 같다.  
그래서 기존 프로젝트를 spm으로 수정하려고 하는데 아무리 가이드대로 해도 아래와 같은 에러가 떴었다.  
  
framework not found  
  
그래서 찾아보니 Build Settings의 Other Linker Flags에 기존것이 남아 있어서 생긴 문제였다.  
사용하고 있는 라이브러리가 Alamofire라고 예를 들면 아래와 같이 등록되어 있는것이 있을것이다.
  
-framework  
"Alamofire"  
  
spm에서 사용하려면 삭제해주면 된다.
