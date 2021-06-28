---
title: "Failed: Not hittable"
categories: 
  - ios
toc: true
---

## Failed: Not hittable
  
XCUITest 코드를 작성 중  
tap을 하려는데 tap이 안되는 경우 아래 extension을 작성해 해결했다
  
  
```swift
extension XCUIElement {
    func forceTapElement() {
        if self.isHittable {
            self.tap()
        }
        else {
            let coordinate: XCUICoordinate = self.coordinate(withNormalizedOffset: CGVector(dx:0.0, dy:0.0))
            coordinate.tap()
        }
    }
}
```
  
아래 스택오버플로우 글을 참고했다  
(https://stackoverflow.com/questions/33422681/xcode-ui-test-ui-testing-failure-failed-to-scroll-to-visible-by-ax-action/33534187)  
  
하지만 결국 내가 원하는 동작이 아닌 다른동작을 했다..
(웹뷰의 링크를 누르는 것이었는데 자꾸 다른 링크를 눌렀다. 아마도 웹의 형태가 영역이 겹치는 경우 이런일이 생기는것 같다.)  
  
일단 접어두고.. appium을 알아봐야할 것 같다. ㅜㅜ