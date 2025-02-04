---
title: "Android Foldable Device Check"
categories: 
  - Android
toc: true
---
  
## Android Foldable Device Check
  
안드로이드 앱 개발을 하다보면 최근 폴더블폰이 많이 생겼다.  
단순 폴더블 폰일때 체크하는 코드는 아래와 같다.

```kotlin

    suspend fun isFoldableDevice(activity: Activity): Boolean {
        val windowInfoTracker = WindowInfoTracker.getOrCreate(activity)
        val layoutInfo = windowInfoTracker.windowLayoutInfo(activity).firstOrNull()

        return layoutInfo?.displayFeatures?.any { it is FoldingFeature } == true
    }

```